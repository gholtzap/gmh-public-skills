# Playwright checks

Use the existing Playwright setup and `expectUI` from `lintapple/playwright` when checking pages that require login or actions. Consult the installed package documentation for its supported API.

## Cover the required states

The helper checks only the current page, state, and viewport. It does not navigate, sign in, or run a viewport or theme matrix for you.

- Configure mobile, desktop, and supported themes in the tests or projects.
- Navigate, sign in, and perform the required actions through the existing test setup.
- Assert that the intended state is ready, then call `expectUI` after each relevant state change. For a deliberate loading or error check, assert that specific state before checking it.

## Inspect failures

Findings fail `expectUI` and produce a `lintapple findings` JSON attachment. Invalid policies, timeouts, and execution errors can also fail a test. Inspect the assertion details and attachments before classifying the failure. Do not catch assertion errors to make a test pass.

Keep the Playwright report and attachments as evidence of the states, sizes, and themes exercised.
