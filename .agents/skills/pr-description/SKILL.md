---
name: pr-description
description: Draft or revise a pull request body from the actual change and available evidence, in gmh's direct, user-first style. Use for PR descriptions, not title-only requests.
---

# Write a PR description like gmh

Explain the change to a reader who has not used this part of the product. The description must make sense without a separate explanation in chat.

## Ground the description

- Read the final diff and available PR context, user notes, tests, and captured results. Identify the problem or goal, the resulting behavior, and the cause or design decision when relevant.
- Describe the final change. Leave out abandoned approaches, authoring history, and file inventories. Include an implementation detail only when it explains the result or a decision the reviewer must assess.
- Preserve wording the user has approved, including concrete examples. Do not replace it with internal terms. Keep useful links, prerequisites, and required checkboxes; remove material the user has rejected.
- For performance, cost, or capacity changes, retain the strongest verified before/after measurements, with units, workload, and relevant conditions or limits. Keep a short result even when linking to evidence. Do not replace measured gains with test counts, present targets as results, or generalize beyond the measured scope.
- Never invent tests, screenshots, outputs, incidents, issue links, or rollout facts. If evidence is thin, make the description thinner. A draft does not authorize publishing or rollout work.

## Explain the problem and result

Lead with the problem or goal and the resulting behavior. For a fix, explain the affected action and what changes. For a feature, explain what someone can now do. For refactoring or infrastructure work, explain the maintenance or operational benefit and any behavior changes. Describe the result before implementation details. Explain a cause only when it helps the reader understand the change or assess a decision.

Use terms the reader can understand without knowing the code. Say "the colours you chose" before introducing an internal name such as "palette B". Explain a product term when it is needed to follow the action.

Keep concrete details that help the reader picture the result. A light mint background with teal buttons is more useful than an unexplained letter. Describe the failure at the useful level: "switches to another unrelated theme" is enough when the exact wrong colours do not affect the explanation. Keep exact values when they define the bug.

A short Before the fix / After the fix block can make the difference clear. Distinguish explanatory examples from captured results. Do not present an invented example as an observed incident.

Use this approved example as a model for plain language, not as a fixed template:

> You choose a light mint background with teal buttons, then click **All previews** to see those colours on different website designs.
>
> **Before the fix:** the previews switch to another unrelated theme.
>
> **After the fix:** the previews keep your light mint background and teal buttons.

For new functionality, state what someone can now do. Give a concrete example when it helps. Introduce terms such as normalization or reconciliation only after the reader understands the problem. Mention older API behavior, a migration, a flag default, or a dependency only when it explains an important decision.

## Keep the shape small

- A small fix can take one to three sentences. A moderate change can use a few short paragraphs and one revealing example. A larger change can use flat bullets for distinct behavior changes. This is a reasoning sequence, not a fixed template.
- Use a direct conversational voice, plain words, contractions, and specific verbs. Casual fragments or first person are fine when natural. Do not force lowercase or typos.
- Do not add `Testing`, `Test plan`, or `Rollout/revert plan` sections by default, including the same boilerplate under another name. Add them only when the user or a repository instruction requires them; an optional template is not a requirement.
- Include one short validation statement when it materially helps the reviewer assess the change. Leave out routine test logs, commands, viewport sizes, and verification links unless requested, required, or necessary to understand that evidence. Perform required checks and keep detailed records separately. State material limitations briefly.
- For stacked work, link actual prerequisites or follow-ups and state the stack position. Leave out routine deploy and revert instructions, generic scope disclaimers, repeated conclusions, and edge-case inventories. Keep an edge case only if it defines behavior a reviewer needs to understand.

## Use evidence that shows the result

Choose the smallest useful evidence that supports the claim. A concise input and before/after example may explain the change; claims about actual execution need captured results. A generated or intercepted message proves its content, not delivery or rendering. Do not add weak evidence merely to fill a section.

When creating or revising screenshots, videos, or their captions, use [PR visual evidence](../pr-visual-evidence/SKILL.md) if available. The evidence must show the same behavior described in the PR. If that skill is unavailable, keep captions understandable on their own and inspect the finished media before attaching it.

Keep required review-app data separate from the explanation. Preserve the parser's expected fields and code fence. If the format supports it, put this machine data in a collapsed section with a clear label. Do not remove it just because it is not useful prose, and do not use it as a substitute for an explanation.

Use multiple examples only when they explain distinct cases. Label them clearly for the reader; no fixed numbering or heading format is required.

Return the PR body unless the user asks for another format. Do not add a separate account of how you wrote it.
