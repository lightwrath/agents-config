---
name: workflow-implement-autonomous
description: Start and facilitate the autonomous implementation segment of the development workflow (Segment 3, Phase 1). The AI follows the plans autonomously without asking questions.
---

# Instructions

Execute the **Implementation Segment** (Segment 3) of the development workflow in **non-interactive (autonomous) mode**.

In this mode, the AI works through the implementation independently, following the plans established in prior segments. **Do not ask the developer questions. Do not pause for confirmation. Do not prompt for decisions.** If something is ambiguous, make a reasonable decision based on existing context, note it in the handoff notes, and continue.

**Operational constraints:**
- Stay within the working directory at all times. Do not access paths outside the project.
- Do not run commands that require elevated privileges, additional authentication, or system-level access.
- Do not install global packages, modify system configuration, or interact with external services outside of what is already configured in the project.
- If a step would require leaving the working directory or triggering a permission check, skip it, document the blocker in the handoff notes, and move on to the next task.

Work through the phase below, using the todo list to track progress.

---

### Implementation Segment (Non-Interactive)

#### Phase 1 — Implementation

Work through the Task Queue in `workflow_tracking.md` in order, tackling one task at a time. For each task:
- Implement only what is needed to make the current test pass
- Build the application and run the test suite
- Mark the task as `[x]` in `workflow_tracking.md` and update the handoff notes at the end of the session, before closing
- Once the build and tests are passing, commit the changes for that task

If a build or test failure cannot be resolved without leaving the working directory or requiring external access, document the blocker in the handoff notes and stop. Do not attempt workarounds that violate the operational constraints above.

**Checkpoint:** All tests must pass and the build must succeed before proceeding to the next segment. Any failures must be resolved before moving on.
