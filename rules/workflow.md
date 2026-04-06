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

## Development Workflow

The workflow is divided into four segments, each facilitated by a dedicated skill:

| Skill | Segment | Phases |
|---|---|---|
| workflow-plan | Segment 1 — Planning | 1–4 |
| workflow-define | Segment 2 — Contract Definition | 1–2 |
| workflow-implement | Segment 3 — Implementation | 1–2 |
| workflow-review | Segment 4 — Review | 1–4 |
