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

---

### Planning Segment

#### Phase 1 — Planning
Define the objective clearly:
- What is being changed or added?
- Why is this change being made?
- What is the desired outcome?

This forms the brief for the rest of the workflow.

**After this phase:** Review `ubiquitous_language.md` and add any new terms that arise from the objective.

---

#### Phase 2 — Exploration
The AI explores the codebase to gather context relevant to the objective:
- Uses LSP capabilities (symbol lookup, find references, type inspection) to understand structure
- Reads relevant files, modules, and interfaces
- Identifies dependencies, constraints, and areas of impact

---

#### Phase 3 — Design Interview
The AI interviews the developer relentlessly about every aspect of the plan until both sides reach a shared understanding. The goal is to walk down each branch of the design tree, resolving dependencies between decisions one by one.

**How it works:**
- The AI identifies every open question, assumption, and decision point in the plan from Phase 1, informed by what was discovered in Phase 2
- Questions are asked one at a time (or in small, focused groups when closely related), starting from the decisions that other decisions depend on
- If a question can be answered by exploring the codebase, the AI investigates first and presents its findings rather than asking the developer
- Each answer narrows the design space — the AI tracks what has been resolved and what remains open
- The interview continues until there are no unresolved branches: every design decision has been made and every dependency between decisions is satisfied

**Principles:**
- No question is too small — surface implicit assumptions early
- Follow dependency order: resolve foundational choices before downstream ones
- Present what you learned from the codebase; only ask the developer what the codebase cannot answer
- Summarise the resolved design tree at the end to confirm shared understanding

No code is written in this phase.

**After this phase:** Write the feature specification document for the vertical slice or module.

---

#### Phase 4 — Planning Wrap-up
Conclude the planning phase before any code is written:
- Review `ubiquitous_language.md` in light of the critique discussions and update any terms that have been refined or added
- Confirm that all criticisms from Phase 3 have been addressed and the agreed approach is clearly reflected in the feature specification document
- Ensure the feature specification document is complete and ready to serve as the source of truth going forward

**Commit:** Commit `ubiquitous_language.md` and the feature specification document. This marks the end of the planning phase — everything that follows is implementation.

---

### Implementation Segment

#### Phase 5 — Interface & Test Definition
Define the contract before implementation:
- Define the interface for the vertical slice or module
- Write the test suite that validates the expected behaviour

**Checkpoint:** The application must still build successfully. The newly defined tests are expected to fail at this stage — this confirms they are correctly targeting behaviour that has not yet been implemented.

---

#### Phase 6 — Prioritisation
Review all failing tests from Phase 5 and produce an `implementation_tasks.md` file within the vertical slice or module folder. This file orders the tests from simplest (least change required) to most complex (e.g., end-to-end tests that exercise the full feature).

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

#### Phase 7 — Implementation
Work through `implementation_tasks.md` in order, tackling one task at a time. For each task:
- Implement only what is needed to make the current test pass
- Build the application and run the test suite
- Mark the task as complete in `implementation_tasks.md` and update the handoff notes before ending the session
- Once the build and tests are passing, commit the changes for that task

**Checkpoint:** All tests must pass and the build must succeed before proceeding to the next phase. Any failures must be resolved before moving on.

---

### Review Segment

#### Phase 8 — Manual Review
The developer reviews the implementation:
- Read through all changes
- Make any manual edits as needed
- Review any manual changes that were required and run the `remember-manual-changes` skill to analyse the alterations and distil them into new or improved rules in `coding_conventions.md`

---

#### Phase 9 — AI Code Review
The AI performs a comprehensive code review of the feature and all related changes:
- Review for correctness, clarity, consistency, and adherence to conventions
- Produce a list of findings

Developer and AI go through the findings together. Any items that need resolving must be addressed before proceeding.

---

#### Phase 10 — Commit
Before committing, run the full test suite and build the application one final time.

**Checkpoint:** All tests must pass and the build must succeed. Any failures must be resolved before the commit is made.

Once the checkpoint is green, commit the changes.
