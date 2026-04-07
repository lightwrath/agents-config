---
name: workflow-implement
description: Start and facilitate the implementation segment of the development workflow (Segment 3, Phases 1–2).
---

# Instructions

Guide the developer through the **Implementation Segment** (Segment 3) of the development workflow.

Work through each phase in order, using the todo list to track progress.

---

### Implementation Segment

#### Phase 1 — Prioritisation
Review all failing tests from Segment 2 and produce an `implementation_tasks.md` file within the vertical slice or module folder. This file orders the tests from simplest (least change required) to most complex (e.g., end-to-end tests that exercise the full feature).

Each task in the file should be treated as an individual unit of work — one failing test to make pass. Between sessions, the AI reads this file to understand current progress and picks up from where the previous session left off.

The file format is as follows:

```markdown
# [Feature Name] — Implementation Tasks

## Agent Handoff Notes
_Use this section to pass context to the next session — decisions made, blockers encountered, and current state._

---

## Task Queue

Complete tasks in order. Mark each as `[x]` before starting the next session.

- [ ] 1. Short description — test type (e.g. unit)
  - File: `path/to/test.ts:line`
  - Notes:
```

---

#### Phase 2 — Implementation
Work through `implementation_tasks.md` in order, tackling one task at a time. For each task:
- Implement only what is needed to make the current test pass
- Build the application and run the test suite
- Mark the task as complete in `implementation_tasks.md` and update the handoff notes before ending the session
- Once the build and tests are passing, commit the changes for that task

**Checkpoint:** All tests must pass and the build must succeed before proceeding to the next segment. Any failures must be resolved before moving on.
