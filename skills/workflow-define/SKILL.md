---
name: workflow-define
description: Start and facilitate the test definition segment of the development workflow (Segment 2, Phases 1–3).
---

# Instructions

Guide the developer through the **Test Definition Segment** (Segment 2) of the development workflow.

Work through each phase in order.

---

### Test Definition Segment

#### Phase 1 — Ubiquitous Language
Review the feature specification and all planning findings, then update `ubiquitous_language.md` at the project root:
- Identify all new domain terms, concepts, and entities introduced by this feature
- Add definitions for each new term, written in plain language that both developer and AI can refer to
- Refine or update any existing terms whose meaning has shifted as a result of the new design

**Checkpoint:** Every meaningful domain concept from the feature specification must have a corresponding entry in `ubiquitous_language.md`.

**Commit:** Commit `ubiquitous_language.md`. This establishes the shared language for the rest of the workflow.

---

#### Phase 2 — Test Definition
Write the tests that define the expected behaviour. **No changes are made to the underlying project** — no interfaces, no implementation stubs, no scaffolding of any kind. Only test files are created or modified.

- Write the test suite that validates the expected behaviour of the feature
- Tests must import from the production code paths they will eventually exercise, but the production code itself is not created or modified here

**Checkpoint:** The tests must exist and target the correct behaviour. They are expected to fail (or fail to compile) at this stage — that is intentional and confirms the tests are correctly pointing at behaviour that has not yet been implemented. Do not attempt to make the project build or the tests pass.

---

#### Phase 3 — Test Review
The developer reviews the defined tests against the feature specification:
- Read through the tests, comparing them against the feature spec
- Make any edits needed to correct or improve them
- The AI assists on request (e.g., "does this test cover this part of the spec?")

No implementation code or production scaffolding is written in this phase.

**Checkpoint:** After the review, the tests are considered locked. Any changes from this point forward require revisiting the feature specification.

**Commit:** Commit the tests. This marks the end of the test definition segment — everything that follows is implementation.
