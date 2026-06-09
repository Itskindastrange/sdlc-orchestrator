---
name: qa-plan-writer
description: Write a QA Plan for any feature or project and commit it as a .md file to the repository. Use this skill whenever the user wants to document test strategy, test cases, coverage targets, or quality assurance planning. Trigger for phrases like "QA plan", "test plan", "test strategy", "write test cases", "what should we test", "testing coverage", "acceptance testing", "how do we QA this", or when a PRD and/or Engineering Design Doc exist and the user is ready to plan quality assurance. Also trigger proactively when a feature is approaching implementation and no test plan exists yet.
---

# QA Plan Writer

Produces a structured, project-tailored QA Plan from the approved PRD and Engineering Design Doc (EDD), then commits it to the repository.

> **Scope of this skill:** The QA Plan is a *quality* document. It answers WHAT gets tested, HOW it gets tested, and WHEN — defining coverage targets, test types, test cases, seams, environments, and pass/fail criteria. It is written after the PRD and EDD are approved, before implementation begins (or in parallel with early implementation). It does NOT restate product requirements or architecture — it references the PRD and EDD and builds on their acceptance criteria and module breakdown.

---

## Step 1: Locate the PRD and EDD

Before writing anything, find both upstream documents. Check in order:

1. Are they in the current conversation context?
2. Are they in the repo at `docs/prd/<feature>.md` and `docs/design/<feature>.md`?
3. Did the user paste or describe them?

**If PRD exists but EDD does not:** Proceed, but note prominently in the QA Plan that the EDD is pending — test cases tied to implementation details may need revision once the EDD is written.

**If neither exists:** Stop. A QA Plan written without a PRD is guesswork. Ask the user to complete the PRD first (`prd-writer` skill) and EDD second (`design-doc-writer` skill).

---

## Step 2: Extract from PRD and EDD

Pull these directly — do not ask the user to repeat them:

**From the PRD:**
- Feature name and problem statement
- User personas and actors
- User stories — these map directly to test scenarios
- Acceptance criteria (Given/When/Then) — these become test cases
- Functional requirements (FR-01, FR-02...) — each must be traceable to at least one test
- Non-functional requirements — performance, security, accessibility targets
- MVP scope — what's in vs. deferred
- Out of scope — don't write tests for these

**From the EDD:**
- Module breakdown — what gets built, what's modified
- API contracts — endpoint specs drive API test cases
- Data model — schema changes drive data integrity tests
- Error handling — failure modes drive negative test cases
- Security considerations — drive security test cases
- Performance targets — drive load test criteria
- Testing strategy section (if present) — incorporate, don't duplicate

---

## Step 3: Assess Testing Context

If a repo is accessible, explore it for:
- Existing test framework and patterns (jest, pytest, RSpec, Cypress, etc.)
- Test directory structure
- Prior art — similar feature tests to use as patterns
- CI/CD pipeline — where tests run, what gates exist
- Existing coverage tooling and thresholds
- Test data management approach (fixtures, factories, seeds, mocks)

---

## Step 4: Resolve QA Ambiguity

Run through this checklist. Ask only what you can't infer from the PRD, EDD, or codebase. Batch into ONE question list.

**Exit condition:** If an answer won't materially change any QA Plan section, skip it. Make stated assumptions and proceed if the user defers.

### Ambiguity Checklist

**Scope & Coverage**
- Is there a minimum coverage target (line, branch, statement)?
- Are there features or flows explicitly excluded from automated testing?

**Test Types**
- Which test types are required: unit, integration, E2E, contract, load, security, accessibility, smoke, regression?
- Is manual testing expected for any flows (exploratory, UAT)?

**Environments**
- What environments exist? (local, dev, staging, prod)
- Where does each test type run?
- Is there a dedicated QA environment?

**Test Data**
- How is test data managed? (fixtures, factories, seeds, sandboxed APIs)
- Is there sensitive/PII data involved that requires anonymization in test environments?

**Ownership**
- Who owns writing the tests — QA engineer, developer, or shared?
- Who owns the QA sign-off before release?

**CI/CD Integration**
- Which test suites must pass before merge?
- Which must pass before deployment to staging? To prod?
- Is there a separate QA gate in the pipeline?

**External Dependencies**
- Are there third-party APIs, services, or queues involved? Are they mockable?
- Is there a contract testing strategy for external integrations?

---

## Step 5: Write the QA Plan

Use the template below. Tailor every section to the project's actual stack and the PRD/EDD requirements. Never leave placeholder text in the final doc. Target length: 2–4 pages for a feature QA Plan.

```markdown
# QA Plan: [Feature Name]

**Status:** Draft | In Review | Approved | Active | Closed
**Version:** 1.0
**Date:** [today]
**Author(s):** [QA engineer / engineer name(s)]
**Reviewers:** [QA lead, engineering lead, PM]
**Approvers:** [QA lead / engineering lead]
**PRD Reference:** [link or path]
**EDD Reference:** [link or path]

---

### Changelog

| Version | Date | Author | Summary |
|---------|------|--------|---------|
| 1.0 | [date] | [author] | Initial draft |

---

## Overview

2–3 sentences: what feature is being tested, what quality bar must be met, and what this plan covers. Not a restatement of the PRD — just enough context for a QA engineer picking this up cold.

---

## Scope

### In Scope
What this QA Plan covers — derived from the PRD's MVP scope and EDD's module breakdown.

- [Module / flow / requirement]
- [Module / flow / requirement]

### Out of Scope
What this QA Plan explicitly does NOT test. Reference PRD Post-MVP deferred items.

- [Thing] — *reason: [deferred / not applicable / covered elsewhere]*

### Requirements Traceability

Every functional requirement from the PRD must map to at least one test case. Track coverage here.

| Requirement ID | Description | Test Case(s) | Status |
|---------------|-------------|-------------|--------|
| FR-01 | [requirement] | TC-001, TC-002 | Covered / Pending / Blocked |
| FR-02 | [requirement] | TC-003 | Covered / Pending / Blocked |

---

## Test Strategy

### Testing Philosophy
What makes a good test for this feature? State the principles that guide test design:

- Test external behavior, not implementation details
- Tests should be deterministic — same input always produces same output
- Prefer testing at the highest seam that gives meaningful coverage
- [Any project-specific principles]

### Test Types & Ownership

| Test Type | Purpose | Owner | When Run | Tool / Framework |
|-----------|---------|-------|----------|-----------------|
| Unit | Test individual functions/components in isolation | Developer | On every commit | [e.g. Jest, pytest] |
| Integration | Test interactions between modules/services | Developer | On every commit | [e.g. Supertest, pytest] |
| E2E | Test complete user flows through the UI | QA / Developer | On PR merge | [e.g. Cypress, Playwright] |
| API | Test endpoint contracts and error responses | Developer / QA | On every commit | [e.g. Postman, pytest] |
| Load / Performance | Validate NFRs under expected and peak load | Developer / QA | Pre-release | [e.g. k6, Locust] |
| Security | Test auth, authz, injection, exposure | QA / Security | Pre-release | [e.g. OWASP ZAP, manual] |
| Accessibility | Validate WCAG compliance | QA / Developer | On PR merge | [e.g. axe, Lighthouse] |
| Smoke | Fast sanity check post-deployment | QA / Ops | Post-deploy | [manual or scripted] |
| Regression | Ensure existing functionality isn't broken | QA | Pre-release | [existing suite] |
| Exploratory / UAT | Human-driven discovery and user acceptance | QA / PM / Stakeholders | Pre-release | Manual |

Only include rows that apply to this feature.

### Test Seams

Where are the boundaries at which this feature will be tested? Prefer existing seams; only introduce new ones if necessary, and at the highest possible level.

| Seam | Level | Description | New or Existing |
|------|-------|-------------|-----------------|
| [e.g. REST API boundary] | Integration | Test via HTTP requests to the API layer | Existing |
| [e.g. UI component] | E2E | Test user flows through the browser | Existing |
| [e.g. Message queue consumer] | Integration | Test event handling in isolation | New |

### Coverage Targets

| Test Type | Target | Current Baseline |
|-----------|--------|-----------------|
| Line coverage | [e.g. ≥ 80%] | [e.g. 74%] |
| Branch coverage | [e.g. ≥ 75%] | [e.g. 68%] |
| Critical path E2E | [e.g. 100% of happy paths] | N/A |
| NFR thresholds | Per NFR table in PRD | N/A |

---

## Test Cases

Group test cases by area. Each test case maps to one or more acceptance criteria from the PRD (Given/When/Then) or a functional/non-functional requirement.

Use this ID format: `TC-[area abbreviation]-[number]` (e.g. TC-AUTH-001, TC-API-003).

### [Area 1: e.g. Authentication]

#### TC-[AREA]-001: [Test case name]
- **Type:** Unit / Integration / E2E / API / etc.
- **Priority:** P0 (must pass for release) / P1 (high) / P2 (medium) / P3 (low)
- **PRD Reference:** AC-[number] / FR-[number]
- **Preconditions:** [State the system must be in before the test runs]
- **Steps:**
  1. [Action]
  2. [Action]
- **Expected result:** [What must be true after the steps complete]
- **Negative / edge variant:** [What happens if input is invalid, missing, or boundary-case]

#### TC-[AREA]-002: [Test case name]
*(repeat for each test case)*

### [Area 2: e.g. API Contracts]

*(repeat structure)*

### [Area N: e.g. Performance]

#### TC-PERF-001: [e.g. p95 response time under normal load]
- **Type:** Load
- **Priority:** P0
- **PRD Reference:** NFR — Performance
- **Tool:** [e.g. k6]
- **Scenario:** [X virtual users, Y requests/sec, Z duration]
- **Pass criteria:** p95 latency < [Xms], error rate < [Y%], no memory leaks detected

---

## Test Data Strategy

- **Approach:** [Fixtures / factories / seeds / anonymized prod snapshot / sandboxed third-party APIs]
- **PII handling:** [How sensitive data is managed in test environments]
- **Setup:** [How test data is created before test runs]
- **Teardown:** [How test data is cleaned up after test runs]
- **External dependencies:** [How third-party services are handled — mocked, stubbed, sandbox env]

---

## Environment Strategy

| Environment | Purpose | Test Types Run Here |
|-------------|---------|---------------------|
| Local | Developer testing during implementation | Unit, integration |
| Dev / CI | Automated gate on every commit/PR | Unit, integration, API |
| Staging | Pre-release validation | E2E, load, security, smoke |
| Production | Post-deploy verification | Smoke only |

---

## CI/CD Integration

| Gate | When | Tests Required to Pass | Blocks? |
|------|------|----------------------|---------|
| PR merge | On every PR | Unit + integration + API | Yes — PR blocked if failing |
| Deploy to staging | On merge to main | Full suite minus load/security | Yes |
| Deploy to prod | After staging sign-off | Smoke tests | Yes |
| Load / security | Pre-release | Load + security tests | Yes — release blocked if failing |

---

## Entry & Exit Criteria

### Entry Criteria (before QA testing begins)
- [ ] PRD and EDD approved
- [ ] Feature implementation complete in staging environment
- [ ] All unit and integration tests passing in CI
- [ ] Test data set up and verified
- [ ] Deployment to staging confirmed

### Exit Criteria (before release sign-off)
- [ ] All P0 test cases passing
- [ ] All P1 test cases passing or risk-accepted with documented justification
- [ ] Coverage targets met
- [ ] NFR thresholds validated (performance, security, accessibility)
- [ ] No open P0 or P1 bugs
- [ ] Exploratory / UAT sign-off from [QA lead / PM / stakeholder]
- [ ] Regression suite passing — no existing functionality broken

---

## Known Risks & Mitigations

| Risk | Impact | Mitigation |
|------|--------|------------|
| [e.g. Third-party API not mockable] | Integration tests may require live sandbox | Use recorded fixtures / VCR pattern |
| [e.g. Load test environment differs from prod] | Results may not reflect real load | Document delta; caveat results |

---

## Open Questions

- [ ] [Question] — *owner: [person], needed by: [date]*

---

## Assumptions

- [Assumption] — *flagged for confirmation by: [owner]*

---

## References

- PRD: [link or path]
- EDD: [link or path]
- Related test files (prior art): [file paths or links]
- Test framework docs: [links]
- CI/CD pipeline config: [link or path]
```

---

## Step 6: Determine Commit Location

| QA Plan type | Path |
|---|---|
| Top-level / whole-product | `docs/qa/QA-PLAN.md` |
| Feature-specific | `docs/qa/<feature-name>.md` |
| Sub-feature | `docs/qa/<feature-name>/<sub-feature>.md` |

The `qa/` folder sits alongside `prd/` and `design/` under `docs/`. Keep them parallel — for every PRD at `docs/prd/X.md` and EDD at `docs/design/X.md`, there should be a QA Plan at `docs/qa/X.md`.

---

## Step 7: Commit to Repository

1. Write the file to the determined path
2. Commit: `docs: add QA plan for <feature name>`
3. For updates: `docs: update QA plan for <feature name> — <what changed>`
4. Confirm the commit path to the user

If no Git access: save locally and tell the user where it is.

---

## Step 8: Post-QA-Plan Handoff (always do this)

After committing, tell the user what comes next:

1. **QA Plan review** — QA lead and engineering lead should review and approve before implementation completes
2. **Test implementation** — developers write unit/integration tests as they build; QA writes E2E and manual test cases
3. **CI/CD integration** — wire test suites into the pipeline gates defined in this plan
4. **Pre-release execution** — run the full suite against staging before any release
5. **ADR** — if significant testing decisions were made (new frameworks, new seams), log them as ADRs in `docs/adr/`

The full SDLC document chain is now complete:
```
PRD → EDD → QA Plan → Implementation → Release
```

---

## Quality Checklist (self-review before committing)

- [ ] PRD and EDD located and referenced — QA Plan does not restate requirements
- [ ] All PRD acceptance criteria mapped to test cases
- [ ] All functional requirements traceable in the Requirements Traceability table
- [ ] NFRs (performance, security, accessibility) have explicit test cases with pass criteria
- [ ] All ambiguity resolved across scope, test types, environments, data, ownership, CI/CD
- [ ] Unresolved items in Assumptions and Open Questions with owners
- [ ] Reviewers and Approvers named in header
- [ ] Changelog present
- [ ] Test seams identified — existing preferred, new ones justified
- [ ] Test cases cover happy paths, negative paths, edge cases, and boundary conditions
- [ ] Test data strategy defined — PII handling addressed if applicable
- [ ] Environment strategy maps test types to the right environment
- [ ] CI/CD gates defined — what blocks merge vs. what blocks release
- [ ] Entry and exit criteria complete and specific
- [ ] Risks documented with mitigations
- [ ] File committed to correct path (`docs/qa/`)
- [ ] Post-QA-Plan handoff communicated to user

---

## Notes

- The Requirements Traceability table is non-negotiable. Every FR from the PRD must appear here. Untraceable requirements are untested requirements.
- P0 test cases must pass before any release, no exceptions. Be deliberate about what gets P0 — not everything is critical path.
- Test seams matter. Testing at too low a level (pure unit tests on internal functions) gives false confidence. Testing at too high a level (only E2E) is slow and brittle. Match the seam to the risk.
- The QA Plan is a living document. Update it when scope changes, when new failure modes are discovered during implementation, or when the EDD changes.
- If the project has no existing test framework, flag this immediately — setting up a test framework is a prerequisite task that needs to be scheduled before test implementation begins.
