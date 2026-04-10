---
name: workflow-implement-autonomous
description: Start and facilitate the autonomous implementation segment of the development workflow (Segment 3, Phases 1–2). The AI follows the plans autonomously without asking questions.
---

# Instructions

Execute the **Implementation Segment** (Segment 3) of the development workflow in **non-interactive (autonomous) mode**.

In this mode, the AI works through the implementation independently, following the plans established in prior segments. **Do not ask the developer questions. Do not pause for confirmation. Do not prompt for decisions.** If something is ambiguous, make a reasonable decision based on existing context, note it in the handoff notes, and continue.

**Operational constraints:**
- Stay within the working directory at all times. Do not access paths outside the project.
- Do not run commands that require elevated privileges, additional authentication, or system-level access.
- Do not install global packages, modify system configuration, or interact with external services outside of what is already configured in the project.
- Do not modify any test files at any time. This applies during implementation and during review. The tests are fixed inputs and must not be edited, replaced, removed, skipped, or weakened.
- If a step would require leaving the working directory or triggering a permission check, skip it, document the blocker in the handoff notes, and move on to the next task.

Work through the phase below and track progress as you go.

---

### Implementation Segment (Non-Interactive)

#### Phase 1 — Implementation

Work through the plan and implement it. Once the implementation work is complete:
- Build the application
- Run the test suite
- Resolve any build failures or failing tests before proceeding
- Record completed work and update the handoff notes at the end of the session, before closing
- Once the build and tests are passing, commit the changes

If a build or test failure cannot be resolved without leaving the working directory or requiring external access, document the blocker in the handoff notes and stop. Do not attempt workarounds that violate the operational constraints above.

**Checkpoint:** The build must succeed and all tests must pass before proceeding. If any test fails, implementation is not complete and work cannot continue until the build and test suite are green.

---

#### Phase 2 — Review

Carry out a review of the whole application after implementation is complete:
- Review the application for correctness, clarity, consistency, and adherence to conventions
- Identify any issues introduced by the implementation
- Resolve the issues you find
- Build the application again
- Run the test suite again

The review must not include modifying tests, and no test files may be changed in this phase.

If review findings cannot be resolved without leaving the working directory or requiring external access, document the blocker in the handoff notes and stop.

**Checkpoint:** The review is only complete when the identified issues have been resolved, the build succeeds, and all tests pass.
