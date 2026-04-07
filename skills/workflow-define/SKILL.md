---
name: workflow-define
description: Start and facilitate the contract definition segment of the development workflow (Segment 2, Phases 1–3).
---

# Instructions

Guide the developer through the **Contract Definition Segment** (Segment 2) of the development workflow.

Work through each phase in order, using the todo list to track progress:
- **Phase 1** produces the scaffold — interfaces and failing tests.
- **Phase 2** is a developer-led review of that scaffold against the feature specification. The AI assists on request. No implementation code is written.
- **Phase 3** orders the failing tests into a prioritised implementation task list, ready for the implementation segment.

---

### Contract Definition Segment

#### Phase 1 — Interface & Test Definition
Define the contract before implementation:
- Define the interface for the vertical slice or module
- Write the test suite that validates the expected behaviour

**Checkpoint:** The application must still build successfully. The newly defined tests are expected to fail at this stage — this confirms they are correctly targeting behaviour that has not yet been implemented.

---

#### Phase 2 — Interface & Test Review
The developer reviews the scaffolded interfaces and tests against the feature specification:
- Read through the interfaces and tests, comparing them against the feature spec
- Make any edits needed to correct or improve them
- The AI assists on request (e.g., "does this interface cover this part of the spec?")

No implementation code is written in this phase.

**Checkpoint:** After the review, the scaffold is considered locked. Any changes from this point forward require revisiting the feature specification.

**Commit:** Commit the interfaces and tests. This marks the end of the contract definition phase — everything that follows is implementation.

---

#### Phase 3 — Prioritisation

Review all failing tests and produce an `implementation_tasks.md` file within the vertical slice or module folder. This file orders the tests from simplest (least change required) to most complex (e.g., end-to-end tests that exercise the full feature).

Each task in the file should be treated as an individual unit of work — one failing test to make pass. Between sessions, the AI reads this file to understand current progress and picks up from where the previous session left off.

The file format is as follows:

```markdown
# [Feature Name] — Implementation Tasks

## Agent Handoff Notes
_Use this section to pass context to the next session — decisions made, blockers encountered, and current state._

---

## Task Queue

Complete tasks in order. Each task is one session. Mark the task as `[x]` at the end of the session in which it was completed, before closing.

- [ ] 1. Short description — test type (e.g. unit)
  - File: `path/to/test.ts:line`
  - Notes:
```
