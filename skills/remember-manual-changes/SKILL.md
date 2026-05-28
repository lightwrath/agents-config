---
name: Remember manual changes
description: Compare generated code to manual changes and update coding convention rules based on the alterations.
---

# Instructions

Investigate the changes that have been made since the initial version was created.
Based on the changes that had to be made from the original version.
Create rules to enforce these practices and add them into the suitable places in `rules/coding_conventions.md`.
Should a rule overlap or already exist then try to improve upon it so the intentions are clearer.
Try to keep rules to a short, single line entry per rule.

This is an auxiliary skill. It can be used during review when manual edits reveal reusable conventions, but it is not required for the standard planning, TDD red, implement, and review flow.

## Example Usage

### Async Patterns
- Always use `async/await`. Never use raw `.then()` promise chains.
