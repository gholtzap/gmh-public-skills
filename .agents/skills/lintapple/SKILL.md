---
name: lintapple
description: Verify web interfaces with Lintapple using the project policy, mobile and desktop sizes, supported themes, and relevant interaction states. Use when starting a web UI change so the policy guides implementation, or when asked to review UI policy, layout, or Lintapple findings. Distinguish findings from incomplete checks.
---

# Lintapple

Use Lintapple to check the changed web UI. Inspect the rendered interface and verify the changed user action as well. A Lintapple pass does not prove good design or correct behavior.

For a review-only request, inspect and report findings without editing the app.

## Read the policy before editing

Read the project `ui-policy.json` before changing UI code. Use that policy for the checks. If the project has no policy, use the package defaults and state this limit.

Inspect the project's existing UI check command, Playwright tests, and report format. Reuse that setup. Use the installed command's help or installed package documentation for options; do not guess flags.

## Check the affected pages and states

- Confirm that the intended route and state are visible before checking. Complete login and wait for the required data, controls, or dialog. Use the installed checker's readiness option or test assertions rather than fixed delays. An unexpected loading screen, login redirect, or error page cannot substitute for the intended page. Deliberately tested loading and error states count as coverage of those states.
- After a frontend change, run the project's UI check command using its configured package manager. Confirm that it covers the affected pages and states; add focused checks for gaps. If there is no project command, run the installed `lintapple` command against each changed page on the local app server.
- Check each changed page at mobile and desktop sizes, in each supported theme and changed state, including open menus, dialogs, loading, errors, and empty results where applicable.
- Use existing Playwright tests when login or actions are required. Read [Playwright checks](references/playwright.md) when using that integration. Check readiness before inspecting each state, and configure the required viewports and themes explicitly.
- During implementation, fix findings caused by the change or needed to complete the requested work, then repeat the affected checks. Report unrelated existing findings without expanding the task. Do not change the policy, remove checks, or add exceptions to make a check pass without an explicit user request.

## Interpret results

For the Lintapple CLI:

| Exit code | Meaning |
| --- | --- |
| 0 | The checker passed for the states it inspected. |
| 1 | UI findings. |
| 2 | The check did not finish. |

For Playwright, use the test result, assertion details, and attachments; CLI exit-code meanings do not apply to its runner.

Report a pass only for pages, states, sizes, and themes successfully checked. Findings, incomplete checks, and other nonzero CLI results do not support a full pass. Existing findings prevent a page-wide pass; untested or blocked coverage remains unverified.

## Keep and report the evidence

Save the JSON reports or Playwright reports and attachments that the checks produce. Report the pages, states, sizes, and themes checked, the command, the CLI exit result or Playwright test result, and the report path.

State any access or setup block and keep completed evidence separate from blocked checks. Follow the project's rules for design and accessibility checks that Lintapple does not cover.
