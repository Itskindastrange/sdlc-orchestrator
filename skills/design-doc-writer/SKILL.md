---
name: design-doc-writer
description: Write an Engineering Design Doc (EDD) for any feature or project and commit it as a .md file to the repository. Use this skill whenever the user wants to document how something will be built — after a PRD exists or is being written. Trigger for phrases like "design doc", "technical spec", "how are we building this", "write up the architecture", "document the implementation", "EDD", "system design", or when the user has a PRD and is ready to plan engineering. Also trigger proactively when implementation decisions, schema changes, or API contracts are being discussed and nothing is documented yet.
---

# Engineering Design Doc Writer

Produces a structured, project-tailored Engineering Design Doc (EDD) from the approved PRD and engineering context, then commits it to the repository.

> **Scope of this skill:** The EDD is an *engineering* document. It answers HOW the system will be built — architecture, modules, data model, API contracts, and key technical decisions. It is written by engineering after the PRD is approved, not before. It does NOT restate product requirements or user stories — those live in the PRD. It references the PRD; it doesn't duplicate it.

---

## Step 1: Locate the PRD

Before writing anything, find the approved PRD. Check in order:

1. Is the PRD in the current conversation context?
2. Is there a `docs/PRD.md` or `docs/prd/<feature>.md` in the repo?
3. Did the user paste or describe it?

If no PRD exists: **stop and tell the user.** An EDD written without an approved PRD will drift. Ask them to write the PRD first (use the `prd-writer` skill), or explicitly confirm they want to proceed without one — in which case, note the risk prominently in the EDD header.

---

## Step 2: Read and Extract from the PRD

Pull these directly from the PRD — do not ask the user to repeat them:

- Feature name and problem being solved
- Functional requirements (FR-01, FR-02, etc.)
- Non-functional requirements (performance, security, scalability, etc.)
- MVP scope — what's in, what's deferred
- Actors and their interactions with the system
- Known dependencies and constraints
- Acceptance criteria — these drive the test seams

Use the PRD's language and terminology throughout the EDD. Consistency across documents matters.

---

## Step 3: Assess Engineering Context

Check what's already known about the project's tech context. If a repo is accessible:

- Explore the codebase: directory structure, existing modules, patterns in use
- Identify ADRs (Architectural Decision Records) — respect existing decisions unless explicitly revisiting them
- Note the stack: languages, frameworks, databases, infra, external services
- Find similar prior implementations to use as patterns

If no repo access, ask in one batch (Step 4).

---

## Step 4: Resolve Engineering Ambiguity

Run through this checklist. Ask only what you genuinely don't know and can't infer from the PRD or codebase. Batch into ONE question list — no drip-feeding.

**Exit condition:** If an answer won't materially change any EDD section, skip it. If the user says "use your judgment," make a stated assumption, document it under Assumptions, and proceed.

### Ambiguity Checklist

**Stack & Environment**
- What is the tech stack? (language, framework, DB, infra, cloud provider)
- Are there existing services/modules this feature plugs into?
- Any hard constraints on technology choices?

**Architecture**
- Greenfield or extending existing architecture?
- Sync or async processing? Event-driven or request/response?
- Monolith, microservices, or serverless?

**Data**
- Where does the data live? New tables/collections, or extending existing schema?
- Any data migration required?
- Data ownership — who writes, who reads?

**APIs & Contracts**
- New endpoints or modifying existing ones?
- Internal API or external/public-facing?
- Any third-party integrations?

**Scale & Performance**
- Expected load (requests/sec, data volume, concurrency)?
- Any caching strategy needed?

**Security**
- Authentication/authorization model?
- Any sensitive data handling (PII, credentials, financial)?

**Deployment**
- How does this deploy? CI/CD pipeline already exists?
- Any infra changes needed (new services, queues, storage)?

---

## Step 5: Write the EDD

Use the template below. Tailor every section to the project's actual stack and the PRD's requirements — never leave placeholder text in the final doc. Target length: 2–5 pages for a feature EDD.

```markdown
# Engineering Design Doc: [Feature Name]

**Status:** Draft | In Review | Approved | Implemented
**Version:** 1.0
**Date:** [today]
**Author(s):** [engineer name(s)]
**Reviewers:** [tech lead, architect, relevant engineers]
**Approvers:** [engineering lead / CTO / whoever signs off]
**PRD Reference:** [link or path to PRD]

---

### Changelog

| Version | Date | Author | Summary |
|---------|------|--------|---------|
| 1.0 | [date] | [author] | Initial draft |

---

## Overview

A 2–3 sentence summary of what this EDD covers, what's being built, and why (referencing the PRD problem). Not a restatement of the PRD — just enough context for an engineer picking this up cold.

---

## Background & Context

What does the engineer need to know about the current system before reading the rest of this doc? Include:

- Relevant existing architecture or modules
- Prior decisions (ADRs) that constrain or inform this work
- Why the current approach is insufficient (in technical terms, not product terms)
- Any prior attempts or prototypes

---

## Goals & Non-Goals

### Engineering Goals
What this implementation must achieve technically. Derive from the PRD's functional and non-functional requirements — but frame in engineering terms.

- [e.g. Expose a new `/api/v1/[resource]` endpoint that satisfies FR-01 through FR-04]
- [e.g. Maintain < 300ms p95 response time under 500 concurrent requests]

### Non-Goals
What this EDD explicitly does NOT address. Reference Post-MVP items from the PRD where relevant.

- [e.g. Multi-tenancy support — deferred to Post-MVP per PRD]
- [e.g. Real-time updates — out of scope, polling only for MVP]

---

## Proposed Architecture

The core technical design. Use diagrams where they help. Describe:

- **System overview:** How does this feature fit into the broader system?
- **Component breakdown:** What are the main components/services/modules, and what does each do?
- **Data flow:** How does data move through the system for the primary use case?
- **Key interactions:** How do components talk to each other (REST, gRPC, events, queues)?

Include a diagram if the flow is non-trivial. ASCII, Mermaid, or link to a diagram tool.

```
[Architecture diagram or description]
```

### Technology Choices

For each non-obvious technology or library choice, state what was chosen and why:

| Decision | Choice | Rationale | Alternatives Considered |
|----------|--------|-----------|------------------------|
| [e.g. Queue system] | [e.g. Kafka] | [e.g. Already in stack, handles required throughput] | [e.g. SQS — ruled out due to vendor lock-in] |

---

## Data Model

### New Tables / Collections / Schemas

For each new data entity:

```
[EntityName]
- field_name: type — description
- field_name: type — description
- indexes: [field(s)]
- constraints: [e.g. unique, not null, FK]
```

### Schema Changes to Existing Entities

| Table / Collection | Change | Reason |
|-------------------|--------|--------|
| [existing entity] | [add/remove/modify field] | [why] |

### Data Migration

Is a migration required? If yes:
- What data needs to be migrated?
- Is it reversible?
- Can it run online (zero-downtime) or does it require maintenance window?
- Estimated migration time and risk

---

## API Design

### New Endpoints

For each new endpoint:

```
[METHOD] /api/v[n]/[resource]

Request:
  Headers: [auth headers, content-type]
  Path params: [param: type — description]
  Query params: [param: type — description]
  Body: {
    field: type — description
  }

Response (200):
  {
    field: type — description
  }

Error responses:
  400: [when / why]
  401: [when / why]
  404: [when / why]
  500: [when / why]

Auth: [required / not required — mechanism]
Rate limiting: [yes/no — limits]
```

### Changes to Existing Endpoints

| Endpoint | Change | Backwards Compatible? |
|----------|--------|-----------------------|
| [endpoint] | [what changes] | Yes / No — [migration plan if no] |

---

## Module Breakdown

What gets built or modified, and who owns it.

| Module / Service | Action | Description | Owner |
|-----------------|--------|-------------|-------|
| [Module name] | New / Modify / Delete | [What it does] | [Team/engineer] |

---

## Key Technical Decisions

The most important engineering decisions made in this design. For each:

**Decision:** [What was decided]
**Context:** [Why this decision had to be made]
**Options considered:**
- Option A: [pros / cons]
- Option B: [pros / cons]
**Chosen:** [Option X — reason]
**Trade-offs accepted:** [What we're giving up]
**Reversibility:** [Easy / Hard / Irreversible — why]

---

## Error Handling & Edge Cases

How does the system behave when things go wrong? Cover:

- **Expected failure modes:** What will fail and how often?
- **Graceful degradation:** What does the system do when a dependency is unavailable?
- **Retry strategy:** For async operations, queues, external calls
- **User-facing errors:** What does the user see? Is it actionable?
- **Logging & alerting:** What gets logged, at what level, and what triggers an alert?

| Failure Scenario | Behavior | User Impact | Alert? |
|-----------------|----------|-------------|--------|
| [e.g. DB connection lost] | [e.g. Return cached data, log error] | [e.g. Stale data shown] | Yes / No |

---

## Security Considerations

- **Authentication:** How are requests authenticated?
- **Authorization:** How is access controlled? Who can do what?
- **Input validation:** Where and how is user input validated/sanitized?
- **Sensitive data:** Is PII, credentials, or financial data involved? How is it handled?
- **Secrets management:** How are API keys, tokens, credentials stored and rotated?
- **Threat vectors:** Any specific attack surfaces to be aware of? (injection, SSRF, etc.)

---

## Performance & Scalability

- **Expected load:** [requests/sec, concurrent users, data volume]
- **Bottlenecks identified:** [where the system could degrade under load]
- **Caching strategy:** [what's cached, where, TTL, invalidation]
- **Database query strategy:** [indexes used, query patterns, N+1 risks]
- **Async / background processing:** [what's offloaded, queue depth management]
- **Scaling approach:** [horizontal / vertical / autoscaling — trigger conditions]

---

## Deployment & Infrastructure

- **Deployment method:** [CI/CD pipeline, manual, feature flag, etc.]
- **Infrastructure changes:** [new services, queues, storage, config]
- **Environment progression:** [local → dev → staging → prod]
- **Feature flags:** [Is this behind a flag? Rollout strategy?]
- **Rollback plan:** [How do we revert if something goes wrong post-deploy?]
- **Zero-downtime requirements:** [Yes/No — approach if yes]

---

## Observability

- **Metrics:** What metrics will be tracked? (latency, error rate, throughput, business KPIs)
- **Logging:** What is logged at what level? Structured logging format?
- **Tracing:** Distributed tracing needed? (e.g. OpenTelemetry)
- **Dashboards:** New dashboard needed, or adding to existing?
- **Alerts:** What conditions trigger alerts, and who gets paged?

---

## Testing Strategy

- **Unit tests:** What logic gets unit-tested? What's the pattern in the codebase?
- **Integration tests:** Which service boundaries get integration-tested?
- **E2E tests:** Is E2E coverage needed? Which flows?
- **Load / performance tests:** Required before launch? Threshold criteria?
- **Test data:** How is test data managed? Fixtures, factories, seeds?
- **Prior art:** Which existing tests are closest in pattern to what's needed here?

> Full QA plan (test cases, seam definitions, coverage targets) is maintained in a separate QA Plan document.

---

## Open Questions

Unresolved technical decisions that must be answered before or during implementation.

- [ ] [Question] — *owner: [engineer], needed by: [date]*

---

## Assumptions

Technical assumptions made in this design that have not been validated.

- [Assumption] — *flagged for confirmation by: [owner]*

---

## Out of Scope

What this EDD does NOT cover. Reference the PRD's Post-MVP list where relevant.

- [Thing] — *rationale / PRD reference*

---

## References

- PRD: [link or path]
- Related ADRs: [links]
- Prior art / similar implementations: [links or file paths]
- External docs (API references, library docs): [links]
```

---

## Step 6: Determine Commit Location

| EDD type | Path |
|---|---|
| Top-level / whole-product design | `docs/design/DESIGN.md` |
| Feature-specific EDD | `docs/design/<feature-name>.md` |
| Sub-feature EDD | `docs/design/<feature-name>/<sub-feature>.md` |

The `design/` folder sits alongside `prd/` under `docs/`. Keep them parallel — for every PRD at `docs/prd/X.md` there should be an EDD at `docs/design/X.md`.

---

## Step 7: Commit to Repository

1. Write the file to the determined path
2. Commit: `docs: add design doc for <feature name>`
3. For updates: `docs: update design doc for <feature name> — <what changed>`
4. Confirm the commit path to the user

If no Git access: save locally and tell the user where it is.

---

## Step 8: Post-EDD Handoff (always do this)

After committing, tell the user what comes next:

1. **EDD Review** — tech lead / architect should review and approve before implementation starts
2. **QA Plan** — test strategy, seams, test types, coverage targets, written by QA or engineering *(skill: `qa-plan-writer` — not yet built)*
3. **Implementation** — engineers pick up tasks derived from the Module Breakdown section
4. **ADR** — if any significant architectural decisions were made, log them as ADRs in `docs/adr/`

---

## Quality Checklist (self-review before committing)

- [ ] PRD located and referenced — EDD does not restate product requirements
- [ ] All ambiguity resolved across stack, architecture, data, APIs, scale, security, deployment
- [ ] Unresolved items in Assumptions and Open Questions with owners
- [ ] Reviewers and Approvers named in header
- [ ] Changelog present
- [ ] Architecture section describes the full system flow clearly
- [ ] Technology choices justified with alternatives considered
- [ ] Data model covers all new and modified entities; migration addressed if needed
- [ ] All new API endpoints fully specified (request, response, errors, auth)
- [ ] Module breakdown is actionable — an engineer can pick up a module and start
- [ ] Key Technical Decisions documented with context, options, trade-offs, reversibility
- [ ] Error handling covers failure modes, degradation, retry, alerting
- [ ] Security covers auth, authz, input validation, sensitive data, secrets
- [ ] Performance section addresses load, bottlenecks, caching, scaling
- [ ] Deployment covers CI/CD, infra changes, rollback plan
- [ ] Observability covers metrics, logging, tracing, alerts
- [ ] Testing strategy present; full QA plan deferred to QA Plan doc
- [ ] Post-MVP / out-of-scope items explicitly noted
- [ ] References section links to PRD and relevant ADRs
- [ ] File committed to correct path (`docs/design/`)
- [ ] Post-EDD handoff communicated to user

---

## Notes

- The EDD is an engineering document. Product managers read it to understand the approach; engineers use it to build. Write for both audiences but optimize for engineers.
- Key Technical Decisions is the most valuable section. Don't skip it or make it superficial — future engineers will thank you for documenting why decisions were made, not just what was decided.
- If a decision is irreversible or expensive to reverse, flag it explicitly. These deserve extra review attention.
- EDDs are versioned with the changelog — don't create new files for revisions.
- If significant architectural decisions emerge during implementation that weren't in the EDD, update the EDD and log an ADR.
