---
name: planning
description: Create markdown and Mermaid HTML planning files for a change.
---

# Instructions

Guide the developer through a planning process that produces a complete set of plan files for a proposed change.

No code is written during this skill.

The output of the skill is:
- A markdown plan file that serves as the written source of truth for the change.
- An HTML diagram file that uses Mermaid.js to visualize the current system and planned changes.

Use clear, project-appropriate file names for the artifacts. Prefer colocating them with the relevant feature, vertical slice, or module documentation when such a location exists. Otherwise, place them in the most appropriate planning or documentation location already used by the project.

---

### Planning Process

#### Phase 1 - Planning
Define the objective clearly:
- What is being changed or added?
- Why is this change being made?
- What is the desired outcome?

This forms the brief for the rest of the planning process.

---

#### Phase 2 - Exploration
The AI explores the codebase to gather context relevant to the objective:
- Uses LSP capabilities where available, including symbol lookup, find references, and type inspection, to understand structure.
- Reads relevant files, modules, interfaces, routes, components, tests, and documentation.
- Identifies dependencies, constraints, existing flows, and areas of impact.

If the change modifies an existing feature, create an initial Mermaid diagram that shows the current state of the system before changes are made. This current-state diagram should capture the relevant components, dependencies, data flow, user flow, or process flow needed to understand the planned modification.

The current-state diagram may be drafted during this phase and finalized in Phase 4 as part of the HTML diagram file.

---

#### Phase 3 - Design Interview
The AI interviews the developer relentlessly about every aspect of the plan until both sides reach a shared understanding. The goal is to walk down each branch of the design tree, resolving dependencies between decisions one by one.

**How it works:**
- The AI identifies every open question, assumption, and decision point in the plan from Phase 1, informed by what was discovered in Phase 2.
- Questions are asked one at a time, or in small focused groups when closely related, starting from the decisions that other decisions depend on.
- If a question can be answered by exploring the codebase, the AI investigates first and presents its findings rather than asking the developer.
- Each answer narrows the design space. The AI tracks what has been resolved and what remains open.
- The interview continues until there are no unresolved branches: every design decision has been made and every dependency between decisions is satisfied.

**Principles:**
- No question is too small; surface implicit assumptions early.
- Follow dependency order: resolve foundational choices before downstream ones.
- Present what was learned from the codebase; only ask the developer what the codebase cannot answer.
- Summarize the resolved design tree at the end to confirm shared understanding.

---

#### Phase 4 - Plan Write-up
Write out the complete markdown plan artifact.

The markdown plan file must include:
- Objective and rationale.
- Desired outcome.
- Current-state findings from exploration.
- Relevant constraints, dependencies, and areas of impact.
- Design decisions made during the Design Interview, including reasoning behind each choice.
- Resolved questions and their outcomes.
- Required implementation changes, grouped by affected feature, module, layer, or file area.
- Testing and verification considerations.
- Risks, edge cases, and follow-up work if any.

The markdown plan should be complete enough to serve as the source of truth for `tdd-red`, `implement`, and `review` when those skills are used.

---

#### Phase 5 - Diagram Write-up
Create the Mermaid HTML diagram artifact.

Planning mode cannot write the HTML diagram file. Switch to code mode before creating the file, then write it with a suitable name to `diagrams/<file>.html` in the current working directory.

The HTML diagram file must:
- Load Mermaid.js from a CDN.
- Render at least one Mermaid diagram visualizing the planned change.
- Include the current-state diagram if Phase 2 identified that an existing feature is being modified.
- Include a planned-state or change-flow diagram that shows the changes needed to reach the desired outcome.
- Be readable as a standalone artifact in a browser.

The diagram content should be consistent with the markdown plan. Keep the diagrams focused on the parts of the system relevant to the change rather than attempting to model the entire application.

At the end, provide only a concise summary of the produced planning artifacts and the key decisions captured.
