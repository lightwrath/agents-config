---
name: workflow-define
description: Start and facilitate the contract definition segment of the development workflow (Segment 2, Phases 1–5).
---

# Instructions

Guide the developer through the **Contract Definition Segment** (Segment 2) of the development workflow.

Work through each phase in order, using the todo list to track progress:
- **Phase 1** creates the workflow tracking file for this feature.
- **Phase 2** establishes the ubiquitous language for the feature.
- **Phase 3** defines the failing tests only — no changes to the underlying project are made.
- **Phase 4** is a developer-led review of the defined tests against the feature specification. The AI assists on request. No implementation code is written.
- **Phase 5** orders the failing tests into a prioritised implementation task list, ready for the implementation segment.

---

### Contract Definition Segment

#### Phase 1 — Setup
Create a `workflow_tracking.md` file at the project root (if one does not already exist) to serve as the persistent reference point for the current workflow session.

The file must record the location of the plan file being worked on. Use the following format:

```markdown
# Workflow Tracking

## Current Plan
- **Plan file:** `path/to/plan.md`
```

If `workflow_tracking.md` already exists, clear its contents first, then write the new content from scratch reflecting the plan file for the current feature.

**Commit:** Commit `workflow_tracking.md`. This anchors the session to a specific plan before any contract work begins.

---

#### Phase 2 — Ubiquitous Language
Review the feature specification and all planning findings, then update `ubiquitous_language.md` at the project root:
- Identify all new domain terms, concepts, and entities introduced by this feature
- Add definitions for each new term, written in plain language that both developer and AI can refer to
- Refine or update any existing terms whose meaning has shifted as a result of the new design

**Checkpoint:** Every meaningful domain concept from the feature specification must have a corresponding entry in `ubiquitous_language.md`.

**Commit:** Commit `ubiquitous_language.md`. This establishes the shared language for the rest of the workflow.

---

#### Phase 3 — Test Definition
Write the tests that define the expected behaviour. **No changes are made to the underlying project** — no interfaces, no implementation stubs, no scaffolding of any kind. Only test files are created or modified.

- Write the test suite that validates the expected behaviour of the feature
- Tests must import from the production code paths they will eventually exercise, but the production code itself is not created or modified here

**Checkpoint:** The tests must exist and target the correct behaviour. They are expected to fail (or fail to compile) at this stage — that is intentional and confirms the tests are correctly pointing at behaviour that has not yet been implemented. Do not attempt to make the project build or the tests pass.

---

#### Phase 4 — Test Review
The developer reviews the defined tests against the feature specification:
- Read through the tests, comparing them against the feature spec
- Make any edits needed to correct or improve them
- The AI assists on request (e.g., "does this test cover this part of the spec?")

No implementation code or production scaffolding is written in this phase.

**Checkpoint:** After the review, the tests are considered locked. Any changes from this point forward require revisiting the feature specification.

**Commit:** Commit the tests. This marks the end of the contract definition phase — everything that follows is implementation.

---

#### Phase 5 — Prioritisation

Review all failing tests and append an implementation task queue to `workflow_tracking.md` at the project root. Order the tasks by estimated implementation effort — not by the complexity of the test itself, but by how much production code needs to be written or changed to make that test pass. The simplest tasks (least implementation work) come first; the most complex (e.g., a test that requires the full feature to be wired together end-to-end) come last.

Each task should be treated as an individual unit of work — one failing test to make pass. Between sessions, the AI reads this file to understand current progress and picks up from where the previous session left off.

Append the following section to `workflow_tracking.md`:

```markdown
## Agent Handoff Notes
_Use this section to pass context to the next session — decisions made, blockers encountered, and current state._

---

## Task Queue

Complete tasks in order. Each task is one session. Mark the task as `[x]` at the end of the session in which it was completed, before closing.

- [ ] 1. Short description — test type (e.g. unit)
  - File: `path/to/test.ts:line`
  - Notes:
```

**Commit:** Commit `workflow_tracking.md`. This marks the end of the contract definition segment.
