# Agentic Development Flow

## Skill Flow

The preferred flow for non-trivial changes is:
1. `planning` - define the objective, explore the codebase, resolve design decisions, and create markdown plus Mermaid HTML planning artifacts.
2. `tdd-red` - define the tests, confirm the test list with the developer, implement only test files, and verify the tests fail for expected red-phase reasons.
3. `implement` - review the plan and failing test baseline, implement the change, get the tests green, refactor toward simplicity and cohesion, then verify the result.
4. `review` - perform a final AI review, update ubiquitous language where needed, run final verification, and commit the reviewed changes.

This flow is flexible rather than mandatory. Use the skills that fit the current task, skip steps that are not useful for the change, and run a skill independently when its inputs already exist.

Avoid mixing responsibilities between skills:
- `planning` creates plan and diagram artifacts; it does not change implementation or tests.
- `tdd-red` edits only test files and verifies the red phase.
- `implement` changes production code to satisfy the approved plan and tests; it does not edit tests.
- `review` handles final review, ubiquitous language updates, final verification, and the normal final commit.

Only the `review` skill commits changes. `implement` must leave implementation changes uncommitted so the final review can inspect the working tree before committing.

---

## Architecture Principles

### Vertical Slices
Features are developed as vertical slices. Each slice spans all necessary layers, such as UI, logic, data, and tests, for a single capability. Work stays contained within the slice's boundaries wherever possible.

When a project is split across multiple layers, such as a separate API and UI project or an additional test project, vertical slices are maintained by using the same folder name for the slice across all projects. For example, a `payments` slice would have a corresponding `payments` folder in the API project, the UI project, and the test project. This ensures the slice remains identifiable and traceable across the entire codebase.

### Modules
When functionality cannot fit cleanly into a vertical slice, such as shared infrastructure or cross-cutting concerns, it is extracted into a module with a clearly defined interface. The module's contract is established before implementation begins.

### Feature Documentation
Each vertical slice or module should include planning artifacts that define the feature's intent, behavior, constraints, and relevant diagrams. These artifacts serve as the source of truth during TDD, implementation, and review.

---

## Ubiquitous Language
Each project may maintain a `ubiquitous_language.md` file at the project root. This file defines the canonical terms used throughout the project by both developer and AI to ensure shared understanding and consistent communication.

Ubiquitous language is updated during the `review` skill when a completed change introduces new domain terms, changes existing meanings, or reveals that a term should be clarified.
