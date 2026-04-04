# Agentic Development Workflow

## Architecture Principles

### Vertical Slices
Features are developed as vertical slices — each slice spans all necessary layers (UI, logic, data) for a single capability. Work stays contained within the slice's boundaries wherever possible.

When a project is split across multiple layers (e.g., a separate API and UI project, or an additional test project), vertical slices are maintained by using the **same folder name for the slice across all projects**. For example, a `payments` slice would have a corresponding `payments` folder in the API project, the UI project, and the test project. This ensures the slice remains identifiable and traceable across the entire codebase.

### Modules
When functionality cannot fit cleanly into a vertical slice (e.g., shared infrastructure, cross-cutting concerns), it is extracted into a **module** with a clearly defined interface. The module's contract is established before implementation begins.

### Feature Documentation
Each vertical slice or module includes a specification document that defines the feature's intent, behaviour, and constraints. This serves as the source of truth during development and review.

---

## Ubiquitous Language
Each project maintains a `ubiquitous_language.md` file at the project root. This file defines the canonical terms used throughout the project — by both developer and AI — to ensure shared understanding and consistent communication.

---

## Development Phases

### Phase 1 — Planning
Define the objective clearly:
- What is being changed or added?
- Why is this change being made?
- What is the desired outcome?

This forms the brief for the rest of the workflow.

**After this phase:** Review `ubiquitous_language.md` and add any new terms that arise from the objective.

---

### Phase 2 — Exploration
The AI explores the codebase to gather context relevant to the objective:
- Uses LSP capabilities (symbol lookup, find references, type inspection) to understand structure
- Reads relevant files, modules, and interfaces
- Identifies dependencies, constraints, and areas of impact

---

### Phase 3 — Critique
A sparring session between developer and AI:
- Reflect on the plan from Phase 1 against the findings from Phase 2
- Challenge assumptions and raise questions
- Evaluate whether the proposed approach is suitable
- Agree on the implementation strategy before proceeding

No code is written in this phase.

**After this phase:** Write the feature specification document for the vertical slice or module.

---

### Phase 4 — Interface & Test Definition
Define the contract before implementation:
- Define the interface for the vertical slice or module
- Write the test suite that validates the expected behaviour

**Checkpoint:** The application must still build successfully. The newly defined tests are expected to fail at this stage — this confirms they are correctly targeting behaviour that has not yet been implemented.

---

### Phase 5 — Prioritisation
Review all failing tests from Phase 4 and produce an `implementation_tasks.md` file within the vertical slice or module folder. This file orders the tests from simplest (least change required) to most complex (e.g., end-to-end tests that exercise the full feature).

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

### Phase 6 — Implementation
Work through `implementation_tasks.md` in order, tackling one task at a time. For each task:
- Implement only what is needed to make the current test pass
- Build the application and run the test suite
- Mark the task as complete in `implementation_tasks.md` and update the handoff notes before ending the session
- Once the build and tests are passing, commit the changes for that task

**Checkpoint:** All tests must pass and the build must succeed before proceeding to the next phase. Any failures must be resolved before moving on.

---

### Phase 7 — Manual Review
The developer reviews the implementation:
- Read through all changes
- Make any manual edits as needed

---

### Phase 8 — AI Code Review
The AI performs a comprehensive code review of the feature and all related changes:
- Review for correctness, clarity, consistency, and adherence to conventions
- Produce a list of findings

Developer and AI go through the findings together. Any items that need resolving must be addressed before proceeding.

---

### Phase 9 — Commit
Before committing, run the full test suite and build the application one final time.

**Checkpoint:** All tests must pass and the build must succeed. Any failures must be resolved before the commit is made.

Once the checkpoint is green, commit the changes.
