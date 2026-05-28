---
name: implement
description: Implement an approved plan autonomously using a TDD green and blue flow, then build, test, review, and commit the result.
---

# Instructions

Implement an approved plan in autonomous mode.

The AI works through the implementation independently, following the approved plan. **Do not ask the developer questions. Do not pause for confirmation. Do not prompt for decisions.** If something is ambiguous, make a reasonable decision based on the plan and existing codebase context, record it in the final summary, and continue.

**Operational constraints:**
- Stay within the working directory at all times. Do not access paths outside the project.
- Do not run commands that require elevated privileges, additional authentication, or system-level access.
- Do not install global packages, modify system configuration, or interact with external services outside of what is already configured in the project.
- Do not modify any test files at any time. This applies during implementation and during review. The tests are fixed inputs and must not be edited, replaced, removed, skipped, or weakened.
- If a step would require leaving the working directory or triggering a permission check, skip it, document the blocker in the final summary, and move on to the next task.

Work through the phases below and track progress as you go.

---

### Implementation Process

#### Phase 1 - Baseline And Plan Review

Review the approved plan and establish the current test baseline before implementation begins.

The AI should:
- Read the relevant markdown plan files produced by the planning skill.
- Review the Mermaid HTML diagrams produced by the planning skill to understand the current state and planned changes.
- Identify the implementation areas, constraints, expected behavior, and test expectations from the plan.
- Run the relevant tests to establish the current failing state.
- Record all tests that are currently failing, including failure names, commands run, and failure reasons where available.
- Distinguish expected red-phase failures from unrelated pre-existing failures or environment issues.

Do not begin implementation until the plan has been reviewed and the failing test baseline has been recorded.

**Checkpoint:** The implementation scope is understood, and all currently failing tests have been documented.

---

#### Phase 2 - Implementation

Work through the plan and implement it. Once the implementation work is complete:
- Build the application
- Run the test suite
- Resolve any build failures or failing tests before proceeding

If a build or test failure cannot be resolved without leaving the working directory or requiring external access, document the blocker in the final summary and stop. Do not attempt workarounds that violate the operational constraints above.

**Checkpoint:** The build must succeed and all tests must pass before proceeding. If any test fails, implementation is not complete and work cannot continue until the build and test suite are green.

---

#### Phase 3 - Refactor

Carry out the TDD blue phase after the tests are green.

The AI should:
- Explore related parts of the codebase to identify cohesion opportunities, duplicated patterns, or existing abstractions that the implementation should align with.
- Review the implementation for unnecessary complexity, duplication, unclear boundaries, and poor separation of concerns.
- Refactor toward simplicity, clarity, maintainability, and cohesive responsibilities.
- Preserve behavior while improving the structure of the implementation.
- Prefer small, localized refactors over broad rewrites.
- Build the application again after refactoring.
- Run the test suite again after refactoring.

The refactor phase must not include modifying tests, and no test files may be changed in this phase.

If refactor findings cannot be resolved without leaving the working directory or requiring external access, document the blocker in the final summary and stop.

**Checkpoint:** The refactored implementation is simpler or clearer where appropriate, the build succeeds, and all tests pass.

---

#### Phase 4 - Review

Carry out a review of the whole application after implementation is complete:
- Review the application for correctness, clarity, consistency, and adherence to conventions
- Identify any issues introduced by the implementation
- Resolve the issues you find
- Build the application again
- Run the test suite again
- Ensure there are no further modifications needed
- Once the build and tests are passing and review is complete, commit the changes

The review must not include modifying tests, and no test files may be changed in this phase.

If review findings cannot be resolved without leaving the working directory or requiring external access, document the blocker in the final summary and stop.

**Checkpoint:** The review is only complete when the identified issues have been resolved, the build succeeds, all tests pass, no further modifications are needed, and the changes have been committed.

At the end, provide a concise summary of the baseline failures, implementation, refactor work, verification results, review findings, commit created, and any blockers or assumptions.
