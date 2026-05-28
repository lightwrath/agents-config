---
name: review
description: Review completed changes, update ubiquitous language, then verify and commit the result.
---

# Instructions

Review completed implementation work and prepare it for commit.

Work through each phase in order. Resolve any issues discovered during review before moving to the next phase.

---

### Review Process

#### Phase 1 - AI Review

Perform a comprehensive AI review of the completed changes:
- Review correctness, clarity, consistency, maintainability, and adherence to project conventions.
- Review the implementation against the plan files and diagrams where available.
- Identify behavioral regressions, missing edge cases, poor separation of concerns, duplicated logic, unclear naming, and unnecessary complexity.
- Produce a prioritized list of findings with file and line references where possible.
- Resolve any findings that require code changes.

After fixes are made, repeat the review until no blocking findings remain.

**Checkpoint:** The implementation has been reviewed, all blocking findings have been resolved, and any accepted residual risks are documented.

---

#### Phase 2 - Ubiquitous Language

Review the completed changes, plan files, diagrams, and review findings, then update `ubiquitous_language.md` at the project root:
- Identify all new domain terms, concepts, and entities introduced by the change.
- Add definitions for each new term, written in plain language that both developer and AI can refer to.
- Refine or update any existing terms whose meaning shifted as a result of the change.
- Remove or clarify terms that are now misleading because of the completed implementation.

If the project does not have a `ubiquitous_language.md` file, create it at the project root only when the completed change introduces meaningful domain language that should be captured.

**Checkpoint:** Every meaningful domain concept introduced or changed by the implementation has a corresponding entry in `ubiquitous_language.md`, or no ubiquitous language update was needed.

---

#### Phase 3 - Commit

Before committing:
- Run the full test suite.
- Build the application.
- Resolve any failures before proceeding.
- Confirm that no further modifications are needed.

**Checkpoint:** All tests pass, the build succeeds, and the working tree contains only the intended changes.

Once the checkpoint is green, commit any uncommitted changes with a concise message that reflects the purpose of the reviewed work. Do not create an empty commit when there are no uncommitted changes.

At the end, provide a concise summary of review findings, ubiquitous language updates, verification results, commit status, and any residual risks or assumptions.
