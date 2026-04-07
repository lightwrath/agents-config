---
name: workflow-plan
description: Start and facilitate the planning segment of the development workflow (Segment 1, Phases 1–4).
---

# Instructions

Guide the developer through the **Planning Segment** (Segment 1, Phases 1–4) of the development workflow.

Work through each phase in order, using the todo list to track progress. No code is written during this segment.

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

**Commit:** Commit `ubiquitous_language.md` and the feature specification document. This marks the end of the planning phase — everything that follows is defining and implementation.
