---
name: gmh-ui
description: Design, build, or review product UI and dashboards with clear actions, useful results, compact layout, SF Pro type, and Nucleo icons. Use for frontend UI work unless the user gives a different design direction.
---

# GMH UI

Build the smallest complete user task. Make the UI clear before you style it. Follow a different design direction when the user gives one.

## Remove friction before styling

- For a utility, open on the work itself. Do not add a homepage, dashboard, onboarding, or sign-in step before the main action unless the task or access requirements need it. Presentation and marketing pages have a different purpose; follow that purpose when requested.
- Treat “remove every single piece of unnecessary UI or text” as a change to what the screen contains, not just its spacing or font sizes. Remove repeated headings, promotional copy, sample content, summary cards, navigation, and secondary controls that do not help the current task. Do not replace removed clutter with smaller decorative clutter.
- Make each visible element earn its place: does it help the user act, understand important state, avoid an error, or recover? “It might be useful” or “it makes the screen look complete” is not enough.
- Require only the information needed to complete the action. Reveal optional detail through a specific, lightweight control when wanted. Do not make the user dismiss or fill in optional features to proceed.
- Preserve useful hierarchy and context. A short section label or quiet divider can make a sparse screen easier to scan. Remove redundant explanation, not the information that makes controls understandable.

For example, an event poll can begin with an event title and Create, then show the event, sharing action, response controls, and guest list. A later request for a guest-list label or optional date picker adds that specific help; it does not justify restoring the dashboard or extra form fields. This is an example of the decision process, not a layout to copy into every app.

## Content and behavior

- Put the current task, result, or problem first. Make the next action clear, and tell the user what that action will do.
- Name the action, target, result, and consequence where that information affects a decision. Let surrounding context do its share; do not repeat an obvious instruction beside a self-explanatory control.
- Keep prior actions and useful context visible or easy to inspect. Show progress, keep the user's place, and make changes easy to follow.
- Start with the facts needed for the next decision. Put lower-use details in a tab, disclosure, or detail view.
- Reduce clicks, scrolling, typing, and repeated choices. Give each text block, control, image, and motion effect a clear purpose.
- Use the same terms, components, and interaction patterns across related views.
- Make each result useful. For a bug report, give steps to reproduce, the expected and actual results, and evidence that helps a person fix the problem.
- Make every visible control do what its label says. Remove controls and links that do not work.

## Components and layout

- Inspect the existing routes, components, state, and data before adding UI. Reuse a matching component or improve a shared UI part when that makes the current task simpler.
- Prefer the project's existing components and installed libraries. Consult external libraries only when a required component is missing; read [component sources](references/component-sources.md) only then. Check that any selected component supports the required behavior, accessibility, and visual rules.
- Use a 4px spacing grid. Use 8px between related items, 16px between groups, and 24px between main sections. Align related text and controls to shared edges; adjust only when content needs more room.

## Polish the remaining interactions

- The quality bar is polished, distinctive, and beautifully restrained. Put creative work into the task itself, rather than adding more UI around it.
- Do not default to the same generic entrance fades and slides across unrelated elements. Connect motion to the user's action and the relationship between the old and new states; keep idle elements quiet. Choose timing and easing for the interaction, and honor reduced-motion preferences.
- Preserve the user's work through secondary interactions. Opening, cancelling, or saving a picker must not clear another field or submit the main form. Verify the sequence the user actually follows, including entering text before opening a dialog.

## Type and icons

- Use SF Pro as the primary font family. Use regular and medium weights only.
- Use 13px as the base size. Use only 12px, 13px, 14px, 16px, 18px, and 24px. Do not use a size above 24px, including for titles.
- Never make a custom SVG icon. Use `@nucleoicons` for each needed icon, with a 1px stroke. Keep icons quiet and aligned with the 13px base size.
- Keep primary task actions clearly named. For familiar secondary actions, prefer icon buttons with tooltips when the icon clearly identifies the action. Give each icon button an accessible name. On touch screens, show the action label beside the icon or use a text button; do not rely on a hover tooltip.
- Do not use Unicode characters, text symbols, or emoji in place of icons. If `@nucleoicons` is not available, use a clear text label or remove the icon. Do not add an icon package for a control that does not need an icon.
- Avoid terminal-style UI. Use sentence-case sans-serif text; reserve monospace for actual code, JSON, commands, and identifiers. Do not use all-caps labels, eyebrow text, or decorative status metadata.

## Check the result

- Maintain mobile parity at all times. Every UI must support the same tasks on mobile and desktop.

Check the main task from start to finish. Test each visible control and check desktop and mobile widths for clipped text, hidden actions, and lost context. Make a final subtraction pass: remove anything the task does not need, while retaining essential labels, feedback, accessibility, and recovery.

- Complete the workflow with a keyboard. Check that controls are reachable and operable, focus remains visible, and focus returns to a useful place after a dialog closes.
- Check that controls and form fields have accessible names that describe their purpose. Associate field labels with their inputs.
- Check touch controls on mobile. Make their targets large enough and spaced so users can select them without activating nearby controls.
- Increase text size and browser zoom. Check that text remains readable and controls, labels, and actions remain usable without clipping or overlap.

For screenshots and recordings that you share, follow the landscape default and portrait exceptions in [PR visual evidence](../pr-visual-evidence/SKILL.md).
