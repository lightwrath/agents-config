---
name: tdd-red
description: Define, implement, and verify failing tests for the red phase of TDD.
---

# Instructions

Guide the developer through the red phase of TDD for a planned change.

The objective is to turn an existing plan into a focused set of tests, implement those tests, and verify that they fail before any production implementation is written.

Only edit test files during this skill. Do not implement production code, change project code, alter application behavior, or add production scaffolding. If a test cannot compile because the planned production interface does not exist yet, leave the test expressing the intended contract and report the compile failure as an expected red-phase result.

---

### TDD Red Process

#### Phase 1 - Test Definition
Review the plan and relevant codebase context to identify the tests that should be created.

The AI should:
- Read the plan files and diagrams relevant to the change.
- Explore existing tests to understand test style, naming, fixtures, helpers, and conventions.
- Identify the behavior that must be proven by tests before implementation.
- Suggest a focused set of tests that cover the planned behavior, important edge cases, and regression risks.
- Explain why each suggested test matters.

Present the suggested tests to the developer for confirmation before implementation.

The developer must have an opportunity to:
- Approve the proposed tests.
- Add missing tests.
- Remove unnecessary tests.
- Adjust test scope, naming, or priority.

Do not proceed to Phase 2 until the test list is confirmed.

---

#### Phase 2 - Test Implementation
Implement the confirmed tests only.

The AI should:
- Follow the project's existing test conventions and file organization.
- Prefer colocating tests with the affected feature, module, or existing test suite.
- Reuse existing test helpers, fixtures, factories, mocks, and setup patterns where appropriate.
- Keep tests focused on observable behavior rather than implementation details.
- Avoid broad snapshot tests unless the project already uses them for the same kind of behavior.
- Do not modify production behavior, project code, configuration, or non-test scaffolding.

If new test utilities are needed, keep them minimal and test-scoped.

---

#### Phase 3 - Red Verification
Run the relevant tests and verify that the newly implemented tests fail for the expected reasons.

The AI should:
- Run the narrowest relevant test command first.
- Expand to a broader test command only when needed to validate integration with the existing suite.
- Confirm that each new test fails because the planned behavior is not implemented yet.
- Distinguish expected red-phase failures from unrelated failures, broken test setup, compile errors, or environment issues.
- Fix test mistakes if a test fails for the wrong reason, then rerun the relevant tests.

The red phase is complete only when the confirmed tests exist and fail for expected, behavior-related reasons.

At the end, provide a concise summary including:
- The tests that were created.
- The test command that was run.
- The failing results and why they are expected in the red phase.
- Any unrelated failures, blockers, or assumptions discovered.
