---
name: e2e-first-testing
description: Plan tests or prune a test suite. Prefer end-to-end tests for complex behavior, keep isolated tests only when they catch real failures that end-to-end tests miss, and write any needed unit tests before implementation.
---

# E2E-first testing

## New work

- Highly prefer E2E tests as the sole test mechanism for complex features. Test the real user or API path.
- Keep E2E checks repeatable. Reuse existing tests, fixtures, commands, and reports. Record additional setup, inputs, steps, and expected and actual results only when someone needs them to verify or repeat the check.
- Never write a unit test after you write the code it tests. If an isolated test is needed, first write down the relevant failure cases affected by the requested change. Then write a test for failures that E2E tests cannot reliably detect. Write the implementation after the test.
- Keep isolated tests for distinct risks such as security boundaries, failure handling, data integrity, and protocol edge cases when E2E coverage cannot detect them.

## Test-suite cleanup

- Inventory the behavior, E2E coverage, and isolated tests before deleting tests. For a repo-wide audit, divide independent areas among parallel subagents when available.
- Delete an isolated test only when it has no realistic failure that the E2E tests would miss. Do not count source-text assertions or duplicated checks as behavior proof.
- Keep tests that detect a distinct failure. If a test is weak but protects a real gap, add E2E coverage before removing it.
- Update test commands and references after deletion. Run the relevant checks and report what was removed, what remains, and the repeatable E2E evidence.
