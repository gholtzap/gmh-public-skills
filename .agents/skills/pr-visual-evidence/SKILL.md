---
name: pr-visual-evidence
description: Create or revise screenshots and videos that explain what a pull request changes. Use for PR visual evidence, before-and-after captures, and visual examples for user feedback.
---

# PR visual evidence

Show the user action, the problem, and the changed result. A reviewer must be able to explain the change from the media and its caption without a separate explanation in chat. The PR description states the change; the media shows that same change.

## Decide what to show

- Read the actual diff, the affected user path, existing capture helpers, and any approved explanation. Reuse a suitable capture method. Do not build a recording system when the existing tools can do the job.
- Write the user action, the failure, and the fixed result in plain language before recording. Use approved wording. Explain product terms before relying on them. Keep concrete examples that make the result easy to picture.
- Choose screenshots when still images explain the result. Choose video when order, timing, interaction, or recovery is part of the claim. A final screenshot cannot show that an older response arrived after a newer choice. Do not require video for every PR.
- Prefer landscape screenshots and recordings. Use a wide viewport and crop to the relevant actions and result, with readable text. Use portrait when a phone layout, vertical content, or an explicit user request makes it necessary. Keep the source proportions; do not stretch or rotate a portrait capture to make it landscape. Record the reason for a portrait capture with the evidence.
- Choose one clear demonstration for each test case. Do not show alternate crops, layouts, screenshots, or videos of the same case as extra examples. A different example needs a distinct input, action, or condition that tests different behavior; a change of presentation alone does not qualify. If one case explains the change, stop at one.
- Plan only the states needed to show the change: the starting choice, the action that triggers the problem, and the result. For a timing bug, show the order of events and wait for the late event before judging the result.

## Capture the change

- Capture the actual base and PR versions. Keep a local record of their commit IDs, inputs, actions, and capture settings. Keep the same inputs, actions, viewport, and theme before and after unless the change itself requires a difference. Do not change another task's checkout or server to make a capture.
- Make the important choice visible. A clipboard paste, an icon click, or a request completing can be hard to see. Use readable framing, existing focus or hover feedback, or a factual caption to explain the event.
- Use captions for what the viewer must notice. Keep test commands, file paths, and implementation details out of captions. Put recording annotations outside the app image or make them clearly distinct from the product UI.
- Leave out decorative titles, PR numbers, commit-comparison subtitles, and repeated explanations inside the media. Text such as "Keep palette B when opening the gallery" and "Same actions on the base commit and the PR commit" adds nothing when the PR already explains the case. Keep only labels needed to follow an action or distinguish Before from After.
- Show the relevant choice and control, not every setting in the surrounding menu. Keep enough context to understand the action, but crop or simplify the capture when unrelated controls make the result harder to see. Do not alter the app to remove those controls.
- Show the real outcome. Do not recolour the app, stage a false success state, or edit out the failure. If a fixture, intercepted response, or controlled delay is needed, disclose it briefly and limit the claim to what it proves.
- Trim unrelated setup and waiting, but keep timing that explains the behavior. Hold the result long enough to inspect it. Do not set a fixed duration, caption style, audio format, or comparison layout without user feedback or a clear need in this example.
- Make the important content readable where the media will appear in the PR. A full-screen capture that becomes unreadable in the PR body needs a better crop or layout. Preserve enough context to identify the action and result.

## Review the finished media

- Inspect the exported screenshots and play the exported video. Check the starting state, trigger, result, captions, and ending. Check that the media supports every claim. A file that exists or a test that passes does not establish this.
- Check text size, framing, playback, and whether the final state remains visible long enough. Remove unrelated errors, private data, and setup from the scene without concealing a relevant failure.
- Run checks required by the project. Keep detailed commands, dimensions, checker reports, and verification records separate from the PR description unless requested or required. A short validation statement may be included when it materially helps review. State a material coverage limit briefly when it affects the claim.
- If the capture cannot show the claimed result, report that limit. Do not substitute a still image for a sequence and call the sequence verified.

## Attach and hand over

- Publish only within the user's authorized scope. If asked to attach the evidence to the PR, finish the upload and body edit, verify that the hosted images load and videos play, and return the PR link. Do not stop at local files. Preserve unrelated PR content and any existing media metadata contract.
- Keep captions understandable on their own. Describe what the user chooses, what happens, and what changes after the fix. Use `pr-description` if available when revising the surrounding body.
- For GitHub uploads used only in machine data, include source-file links in the collapsed section as well. Links inside a code fence alone may not retain the uploaded files. Check each hosted source URL after saving.
- Keep required review-app metadata separate from the human explanation. Preserve its format and commit association. Use a collapsed section when the existing parser supports that placement; do not add a visible test report to explain the machine data.
- Use several examples only when distinct test cases help explain the change. Label them clearly for the reader; no fixed numbering or heading format is required. Do not add redundant views or examples to reach a count. Before and after versions form one comparison, not two test cases.

## Improve from feedback

Use [references/feedback.md](references/feedback.md) when preparing feedback examples or updating these skills from a correction.

Review a complete draft with the user. Apply corrections to the same example and keep a local copy of the earlier version for comparison. A plan alone cannot establish whether framing, pacing, and explanation work.

When the user asks to incorporate feedback into the skill, turn the correction into the narrowest useful instruction and a concrete example. Distinguish approved wording from unreviewed visual choices. Do not turn one example into a universal rule. Check the revised guidance on a different PR before claiming that it produces reliable results across changes.
