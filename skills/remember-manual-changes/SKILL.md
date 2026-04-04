---
name: Remember manual changes
description: Compare initial generated code to changes made manually and create rules to the agents md file based on the alterations.
---

# Instructions

Investigate the changes that have been made since the initial version was created.
Based on the changes that had to be made from the original version.
Create rules to enforce these practices and add them into the suitable places into the .kilocode/rules/coding_conventions.md file.
Should a rule overlap or already exist then try to improve upon it so the intentions are clearer.
Try to keep rules to a short, single line entry per rule.

## Example Usage

### Async Patterns
- Always use `async/await`. Never use raw `.then()` promise chains.
