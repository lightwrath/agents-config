---
name: workflow-review
description: Start and facilitate the review segment of the development workflow (Segment 4, Phases 1–5).
---

# Instructions

Guide the developer through the **Review Segment** (Segment 4) of the development workflow.

Work through each phase in order, using `workflow_tracking.md` to track progress.

---

### Review Segment

#### Phase 1 — AI Code Review
The AI performs a comprehensive code review of the feature and all related changes:
- Review for correctness, clarity, consistency, and adherence to conventions
- Produce a list of findings

Developer and AI go through the findings together. Any items that need resolving must be addressed before proceeding.

---

#### Phase 2 — Manual Review
No AI actions are needed in this phase. The developer reviews the implementation:
- Read through all changes
- Make any manual edits as needed

The developer will indicate when the manual review is complete.

---

#### Phase 3 — AI Code Review
Run the `remember-manual-changes` skill to analyse the manual alterations and distil them into new or improved rules in `coding_conventions.md`.

The AI then performs a second comprehensive code review covering all changes, including those made during the manual review:
- Review for correctness, clarity, consistency, and adherence to conventions
- Produce a list of findings

Developer and AI go through the findings together. Any items that need resolving must be addressed before proceeding.

---

#### Phase 4 — Cleanup
Delete the following files from the project root:
- `workflow_tracking.md`
- The plan file referenced within `workflow_tracking.md`

These files are no longer needed once the feature has been reviewed and is ready to be committed.

---

#### Phase 5 — Commit
Before committing, run the full test suite and build the application one final time.

**Checkpoint:** All tests must pass and the build must succeed. Any failures must be resolved before the commit is made.

Once the checkpoint is green, commit the changes.
