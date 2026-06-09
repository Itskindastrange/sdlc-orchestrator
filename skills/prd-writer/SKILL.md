---
name: prd-writer
description: Write a PRD (Product Requirements Document) for any project or feature and commit it as a .md file to the repository. Use this skill whenever the user mentions writing a PRD, product spec, requirements doc, or feature doc — even if they just say "write up what we discussed" or "document this feature". Trigger when user says "PRD", "product requirements", "spec this out", "write up the requirements", or starts describing a feature they want documented. Also trigger proactively when a substantial feature discussion has happened and no PRD exists yet.
---

# PRD Writer

Produces a structured, complete, standard-compliant PRD from conversation context or user input, then commits it to the correct location in the repository.

> **Scope of this skill:** The PRD is a *product* document — it defines the problem, users, requirements, and scope. It does NOT contain implementation decisions, test strategy, or a phased roadmap. Those belong in separate post-PRD artifacts (Engineering Design Doc, QA Plan, Roadmap). After committing the PRD, inform the user which post-PRD documents should be written next. See **Post-PRD Handoff** section at the bottom.

---

## Step 1: Assess Context

Before asking anything, check what you already know:

**If a repo/project is configured and accessible:**
- Explore the codebase to understand architecture, domain language, and existing ADRs
- Use the project's vocabulary throughout the PRD (not generic terms)

**If starting fresh (no repo context):**
Ask only what you don't know. Minimum required to proceed:
1. What is the product/project?
2. What feature or problem does this PRD cover?
3. Who are the primary users/actors?
4. Any known constraints, timeline, or out-of-scope items?

Do NOT ask for information you can reasonably infer. If you know the answer, use it.

---

## Step 2: Resolve All Ambiguity Before Writing

A PRD with gaps is worse than no PRD. Before writing a single section, run through this checklist mentally and identify every unknown. Then ask everything in ONE batch — no drip-feeding across turns.

**Rule:** Only ask what you genuinely don't know and can't infer. If fewer than 3 of the 7 dimensions below are answered, fall back to the `doc-coauthoring` skill for guided context gathering, then return here to write.

**Exit condition:** If a question's answer won't materially change any PRD section, don't ask it. If the user gives a partial answer, make a stated assumption and proceed — do not loop back.

### Ambiguity Checklist

**Problem**
- Is the core problem clearly defined from the user's perspective?
- Is the business impact of leaving it unsolved known?

**Users & Actors**
- Is every actor who touches this feature identified?
- Are there admin, ops, or system actors beyond the primary user?

**Scope**
- Is it clear what's in vs. out for this PRD?
- Is there a specific MVP cut, or is scope open-ended?

**Success**
- How will we know this shipped successfully?
- Are there measurable, outcome-based targets?

**Tech / Stack**
- Is the tech stack known, or should the PRD be stack-agnostic?
- Are there architectural constraints or known integrations?

**Constraints**
- Is there a deadline or phased delivery expectation?
- Are there compliance, security, or accessibility requirements?

**Risks & Unknowns**
- Are there known unknowns the team is aware of?
- Are there dependencies on external teams or decisions not yet made?

### How to Ask

Batch all gaps into one numbered list. One thing per question, no compound questions:

> Before I write this, a few things I need to nail down:
> 1. [Question]
> 2. [Question]

Wait for answers. If the user says "use your judgment," make a reasonable assumption, document it under **Assumptions**, and flag it as an open question.

---

## Step 3: Decide Writing Mode

**Rich context** (3+ dimensions answered, substantial conversation history, or repo access):
→ Write the PRD directly. Proceed to Step 4.

**Thin context** (fewer than 3 dimensions answered, starting from scratch, or user wants collaborative drafting):
→ Fall back to `doc-coauthoring` skill for guided section-by-section drafting, then return here for Step 5 (commit).

---

## Step 4: Write the PRD

Use the template below exactly. Be thorough on every section — thin sections are a red flag. Apply domain vocabulary throughout. Target length: 1–3 pages for a feature PRD, longer only for a product-level PRD.

```markdown
# PRD: [Feature Name]

**Status:** Draft | In Review | Approved | Shipped
**Version:** 1.0
**Date:** [today]
**Author:** [name if known]
**Reviewers:** [names / roles who must review]
**Approvers:** [names / roles who must sign off before dev starts]

---

### Changelog

| Version | Date | Author | Summary of Changes |
|---------|------|--------|--------------------|
| 1.0 | [date] | [author] | Initial draft |

---

## Problem Statement

The problem the user is facing, written from their perspective — not from an engineering angle. Describe what's broken, missing, or frustrating. Include who is affected and the business impact of leaving it unsolved.

---

## Solution Overview

The proposed solution, from the user's perspective. Describe the end state, not the implementation. What does "done" look like for the user?

---

## Goals & Success Metrics

Metrics must be measurable and outcome-based. Avoid vanity metrics (page views, downloads) unless tied to a business outcome. Prefer outcome metrics (conversion, retention, error rate, time-on-task) over output metrics (features shipped).

| Goal | Metric | Baseline | Target |
|------|--------|----------|--------|
| [e.g. Reduce onboarding drop-off] | [e.g. % completing step 3] | [e.g. 42%] | [e.g. >70% within 60 days of launch] |

---

## User Personas & Actors

Who interacts with this feature? List every actor — end users, admins, external systems — with their role and primary goal.

- **[Actor 1]:** [Role and goal]
- **[Actor 2]:** [Role and goal]

---

## User Stories

A comprehensive, numbered list grouped by actor. Cover ALL flows: happy paths, edge cases, error states, empty states, admin flows, and permission boundaries.

**Do not cut this list short. A thin User Stories section means the feature isn't fully understood.**

Each story: *As a [actor], I want [feature], so that [benefit].*

### [Actor 1] Stories
1. As a ..., I want ..., so that ...

### [Actor 2] Stories
1. ...

---

## Acceptance Criteria

For each user story (or group of related stories), define the precise, testable conditions that must be true before the feature is considered done.

Format: *Given [context], when [action], then [expected outcome].*

### [Story or group reference]
- Given ..., when ..., then ...
- Given ..., when ..., then ...

**Note:** Acceptance Criteria are the contract between product and engineering. Vague AC = scope creep and missed expectations.

---

## Functional Requirements

What the system must DO. Written as clear, testable statements grouped by area. Each requirement gets a unique ID for traceability.

### [Area / Module]
- **FR-01:** The system shall...
- **FR-02:** The system shall...

### [Area / Module]
- **FR-03:** The system shall...

---

## Non-Functional Requirements

How the system must BEHAVE. Fill in every row that applies; mark N/A for those that genuinely don't apply.

| Category | Requirement |
|----------|-------------|
| **Performance** | e.g. API response < 300ms at p95 under normal load |
| **Scalability** | e.g. Must support up to X concurrent users without degradation |
| **Security** | e.g. All endpoints require authenticated session; PII encrypted at rest |
| **Reliability** | e.g. 99.9% uptime SLA; graceful degradation on dependency failure |
| **Accessibility** | e.g. WCAG 2.1 AA compliance |
| **Compliance** | e.g. GDPR, SOC 2, HIPAA — specify which articles/controls apply |
| **Maintainability** | e.g. A new engineer should be able to extend this module within one day |

---

## Design & UX

- **Figma / Wireframes:** [link or "not yet designed"]
- **Key user flows:** [describe the primary flow or reference a diagram]
- **UX decisions:** [any product-side decisions about the user experience]
- **Accessibility notes:** [specific requirements beyond the NFR above, if any]

---

## MVP Scope

The minimum viable version that delivers real value. Be strict — MVP is the smallest thing that solves the core problem. Everything else is Post-MVP.

### In MVP
- [Capability — one line]
- [Capability]

### Post-MVP (explicitly deferred)
- [Capability] — *reason: [too complex / dependency / low priority]*
- [Capability] — *reason: ...*

> Post-MVP items feed into the product roadmap, which is maintained separately from this PRD.

---

## Dependencies & Risks

### Dependencies
- [Internal or external dependency and how it affects delivery]

### Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| [Risk] | High / Med / Low | High / Med / Low | [Action] |

---

## Open Questions

Unresolved decisions that must be answered before or during development.

- [ ] [Question] — *owner: [person], needed by: [date]*

---

## Out of Scope

Explicitly what this PRD does NOT cover. Be specific — vague "future work" entries are not useful.

- [Thing] — *rationale*

---

## Assumptions

Things assumed to be true that were not explicitly confirmed. Must be validated before or during development.

- [Assumption] — *flagged for confirmation by: [owner]*

---

## Further Notes

Stakeholder context, links to related docs, prior art, research, or conversation threads that informed this PRD.

---

> **Next steps after PRD approval:**
> 1. Engineering Design Doc — architecture, implementation decisions, schema, API contracts
> 2. QA Plan — test strategy, seams, test types, prior art
> 3. Product Roadmap update — slot Post-MVP items into the roadmap
```

---

## Step 5: Determine Commit Location

| PRD type | Path |
|---|---|
| Top-level / whole-product / major initiative | `docs/PRD.md` |
| Specific feature within a larger project | `docs/prd/<feature-name>.md` |
| Sub-feature or iteration on an existing feature | `docs/prd/<feature-name>/<sub-feature>.md` |

Rule of thumb: touches multiple systems or defines product direction → root. Scoped to one feature → `prd/` subfolder.

---

## Step 6: Commit to Repository

1. Write the file to the determined path
2. Commit: `docs: add PRD for <feature name>`
3. For updates to an existing PRD: `docs: update PRD for <feature name> — <what changed>`
4. Confirm the commit path to the user

If no Git access is available, save locally and tell the user where to find it.

---

## Step 7: Post-PRD Handoff (always do this)

After committing, tell the user which documents should be written next, in this order:

1. **Engineering Design Doc** — covers implementation decisions, module breakdown, schema changes, API contracts, architectural decisions. Written by engineering after PRD is approved. *(separate skill: `design-doc-writer` — does not exist yet)*
2. **QA Plan** — covers test strategy, test types, seams, prior art, acceptance test cases. Written by QA/engineering. *(separate skill: `qa-plan-writer` — does not exist yet)*
3. **Roadmap update** — Post-MVP items from this PRD should be slotted into the product roadmap. *(done manually or via a roadmap tool)*

These are intentionally separate from the PRD. The PRD is a product document. Implementation and testing decisions are engineering documents that follow PRD approval — not inputs to it.

---

## Quality Checklist (self-review before committing)

- [ ] All ambiguity resolved before writing across all 7 dimensions
- [ ] Unresolved items captured in Assumptions and Open Questions
- [ ] Reviewers and Approvers named in the header
- [ ] Changelog present
- [ ] Problem Statement is from the user's perspective, not engineering's
- [ ] Solution describes the end state, not the implementation
- [ ] Success Metrics are outcome-based and time-bound — no vanity metrics
- [ ] User Stories cover ALL actors, happy paths, edge cases, errors, admin flows
- [ ] Acceptance Criteria present for all stories — Given/When/Then format
- [ ] Functional Requirements are numbered and testable ("the system shall...")
- [ ] Non-Functional Requirements cover all applicable dimensions
- [ ] Design & UX section references or notes design artifacts
- [ ] MVP Scope is strict; Post-MVP items have rationale
- [ ] Dependencies and Risks documented with mitigations
- [ ] Open Questions have owners and deadlines
- [ ] Out of Scope is specific with rationale
- [ ] No implementation decisions or test strategy in the PRD
- [ ] No phased roadmap table — Post-MVP is a bullet list only
- [ ] Domain vocabulary used throughout
- [ ] File committed to the correct path
- [ ] Post-PRD handoff communicated to user

---

## Notes

- Never ask unnecessary questions. If you can infer it, infer it.
- The User Stories and Acceptance Criteria sections are the most commonly underdeveloped. Push for completeness.
- PRDs are living documents — version them with the changelog, don't create new files for each revision.
- The PRD is approved by stakeholders, then handed to engineering. It does not contain engineering decisions.
