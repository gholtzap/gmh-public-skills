# Feedback examples

## Accepted writing guidance

One reviewed explanation starts with choosing a light mint background with teal buttons and clicking All previews. Before the fix, previews switch to another unrelated theme. After the fix, they keep the chosen background and buttons.

The exact approved paragraph is in the `pr-description` skill. This example establishes plain language, a concrete input, and a useful level of detail about the failure. It does not require colour examples in unrelated PRs.

| User correction | Instruction that follows |
| --- | --- |
| The chat explanation is more helpful than the PR body. | Put that approved explanation in the body. Do not leave the useful context only in chat. |
| The reader does not understand palette B. | Explain the choice and action before using an internal or product-specific name. |
| Keep the mint and teal example. | Keep concrete details that help the reader picture the result. |
| Say another unrelated theme instead of listing the wrong colours. | Omit exact wrong values when they do not affect the explanation. |
| The reader does not want a routine test log. | Keep detailed records separately. Include concise validation evidence when it materially helps review, and retain material limitations. |
| Do not show different views of one example. | Choose the clearest demonstration of the case and omit alternate presentations. |
| Do not provide multiple examples unless needed. | Each additional example must test distinctly different behavior. One case does not need a numbered heading. |
| Remove the heading and commit-comparison subtitle from the screenshot and video. | Omit decorative titles and repeated PR context inside media. Keep only useful action and Before/After labels. |
| The description of the second image does not say what happens. | Explain the actual choice, action, and result rather than listing the parts of the image. |
| Most settings in the palette menu are not relevant. | Show the chosen colours and the All previews action; omit unrelated settings from the framing when possible. |
| What is the JSON block for? | Keep required review-app data separate from the explanation, with a clear label and collapsed display when supported. Preserve the parser contract. |

## Accepted visual guidance

Prefer landscape screenshots and recordings unless portrait is needed to show the issue or the user requests it. In one reviewed filter example, a tall phone recording was rejected because the action and result fit in a shorter landscape view. This is a framing preference, not a reason to omit mobile checks.

An earlier draft presented the same action as a screenshot comparison, a three-step screenshot, a combined video, and separate clips. The user rejected treating these views as different examples. Use one clear demonstration of that case. Do not publish multiple formats of the same case as extra examples.

Show only the content needed to understand the action and result. In the palette menu, the chosen colours and the All previews action matter; unrelated settings add clutter. Remove decorative headings and PR-reference text that repeat the surrounding explanation.

## Visual choices still open

The user has not approved a fixed duration, comparison layout, crop, caption style, or lack of audio as a general preference. The rejection of redundant views does not establish a preferred format for every test case.

Another example concerns an earlier request replacing a later palette choice. A static final screenshot does not show that order. A suitable video must show the first request starting, the newer choice taking effect, the earlier response arriving, and whether the newer choice remains. This supports video for that timing-dependent change, not for every PR.

## Feedback cycle

1. Make a complete draft that the user can view in its intended location.
2. Accept ordinary feedback. A format name or timestamp helps locate the problem but is not required.
3. Revise the same example. Keep the earlier local version when it helps compare the correction.
4. When asked to update the skill, save the narrow instruction and the reason it matters. Keep approved and pending choices distinct.
5. Try the revised guidance on a different kind of PR. Do not claim that success on the original example proves it will work on all PRs.

Possible corrections, not yet approved preferences:

| Feedback | Possible correction to test |
| --- | --- |
| I cannot tell what changed. | Establish the starting choice and identify the changed result. |
| The paste is invisible. | Show or identify the pasted input when the result depends on it. |
| This skips the bug. | Record the trigger and failure, not only the final screen. |
| There is too much waiting. | Cut unrelated delay and keep the delay that explains the bug. |
| The caption claims more than the video shows. | Narrow the claim or make a capture that shows the missing behavior. |
