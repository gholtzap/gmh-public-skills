---
name: gmh-ui
description: Design, build, or review product UI and dashboards with clear actions, useful results, compact layout, SF Pro type, and Nucleo icons. Use for frontend UI work unless the user gives a different design direction.
---

# GMH UI

Build the smallest complete user task. Make the UI clear before you style it. Follow a different design direction when the user gives one.

## Content and behavior

- Put the current task, result, or problem first. Make the next action clear, and tell the user what that action will do.
- Name the action, target, result, and consequence. Remove vague claims and labels.
- Keep prior actions and useful context visible or easy to inspect. Show progress, keep the user's place, and make changes easy to follow.
- Start with the facts needed for the next decision. Put lower-use details in a tab, disclosure, or detail view.
- Reduce clicks, scrolling, typing, and repeated choices. Give each text block, control, image, and motion effect a clear purpose.
- Use the same terms, components, and interaction patterns across related views.
- Make each result useful. For a bug report, give steps to reproduce, the expected and actual results, and evidence that helps a person fix the problem.
- Make every visible control do what its label says. Remove controls and links that do not work.

## Components and layout

- Inspect the existing routes, components, state, and data before adding UI. Reuse a matching component or improve a shared UI part when that makes the current task simpler.
- Prefer the project's existing components and installed libraries. Consult external libraries only when a required component is missing; read [component sources](references/component-sources.md) only then. Check that any selected component supports the required behavior, accessibility, and visual rules.
- Use motion only when it helps the user see a change or result.
- Use a 4px spacing grid. Use 8px between related items, 16px between groups, and 24px between main sections. Align related text and controls to shared edges; adjust only when content needs more room.

## Type and icons

- Use SF Pro as the primary font family. Use regular and medium weights only.
- Use 13px as the base size. Use only 12px, 13px, 14px, 16px, 18px, and 24px. Do not use a size above 24px, including for titles.
- Never make a custom SVG icon. Use `@nucleoicons` for each needed icon, with a 1px stroke. Keep icons quiet and aligned with the 13px base size.
- Prefer icon buttons with tooltips over text buttons when the icon clearly identifies the action. Give each icon button an accessible name. On touch screens, show the action label beside the icon or use a text button; do not rely on a hover tooltip.
- Do not use Unicode characters, text symbols, or emoji in place of icons. If `@nucleoicons` is not available, use a clear text label or remove the icon. Do not add an icon package for a control that does not need an icon.
- Avoid terminal-style UI. Use sentence-case sans-serif text; reserve monospace for actual code, JSON, commands, and identifiers. Do not use all-caps labels, eyebrow text, or decorative status metadata.

## Check the result

- Maintain mobile parity at all times. Every UI must support the same tasks on mobile and desktop.

Check the main task from start to finish. Test each visible control and check desktop and mobile widths for clipped text, hidden actions, and lost context.

- Complete the workflow with a keyboard. Check that controls are reachable and operable, focus remains visible, and focus returns to a useful place after a dialog closes.
- Check that controls and form fields have accessible names that describe their purpose. Associate field labels with their inputs.
- Check touch controls on mobile. Make their targets large enough and spaced so users can select them without activating nearby controls.
- Increase text size and browser zoom. Check that text remains readable and controls, labels, and actions remain usable without clipping or overlap.

For screenshots and recordings that you share, follow the landscape default and portrait exceptions in [PR visual evidence](../pr-visual-evidence/SKILL.md).
