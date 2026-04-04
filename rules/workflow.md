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

### Phase 5 — Implementation
Implement the solution:
- Write the full feature or module
- Build the application and run the test suite

**Checkpoint:** All tests must pass and the build must succeed before proceeding. Any failures must be resolved at this stage.

---

### Phase 6 — Manual Review
The developer reviews the implementation:
- Read through all changes
- Make any manual edits as needed

---

### Phase 7 — AI Code Review
The AI performs a comprehensive code review of the feature and all related changes:
- Review for correctness, clarity, consistency, and adherence to conventions
- Produce a list of findings

Developer and AI go through the findings together. Any items that need resolving must be addressed before proceeding.

---

### Phase 8 — Commit
Before committing, run the full test suite and build the application one final time.

**Checkpoint:** All tests must pass and the build must succeed. Any failures must be resolved before the commit is made.

Once the checkpoint is green, commit the changes.
