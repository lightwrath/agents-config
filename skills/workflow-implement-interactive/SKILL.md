---
name: workflow-implement-interactive
description: Start and facilitate the interactive implementation segment of the development workflow (Segment 3, Phase 1), where the AI and developer work through the implementation together.
---

# Instructions

Guide the developer through the **Implementation Segment** (Segment 3) of the development workflow in **interactive mode**.

In this mode, the AI and the developer are working as a pair. The AI proposes, the developer decides. Every significant step — task ordering, implementation approach, design choices, ambiguities — is discussed and agreed upon before proceeding. Neither party moves forward alone.

**Pause and check in with the developer at the end of each task before moving to the next.**

---

### Implementation Segment (Interactive)

#### Phase 1 — Implementation (Paired)

Work through the implementation tasks in order, one task at a time. For each task, the AI and developer work together:

1. **Discuss before implementing** — the AI describes its intended approach for the task. The developer reviews and confirms, suggests changes, or flags concerns before any code is written.
2. **Implement together** — the AI writes the implementation. The developer reviews each change as it is made. If the developer raises a concern mid-implementation, stop and discuss before continuing.
3. **Verify together** — build the application and run the test suite. Both parties review the output. If tests fail, discuss the failure and the fix before proceeding.
4. **Agree before committing** — the AI proposes a commit message. The developer approves before the commit is made.
5. **Record progress** — note completed work and update the handoff notes at the end of the session, before closing. Confirm with the developer before doing so.

**At no point should the AI move to the next task without the developer's acknowledgement that the current task is complete.**

**Checkpoint:** All tests must pass and the build must succeed before proceeding to the next segment. Both the AI and the developer must agree that the implementation is ready before moving on. Any failures or concerns from either party must be resolved first.
