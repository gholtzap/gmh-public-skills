# Engineering guidance

Follow the user's scope and the project's existing contracts and conventions. Read each applicable `SKILL.md` before using it, and load only references needed for the task.

| Task | Skill |
| --- | --- |
| Software design, implementation, refactoring, or review | [general-software-engineering](.agents/skills/general-software-engineering/SKILL.md) |
| Product UI design or changes | [gmh-ui](.agents/skills/gmh-ui/SKILL.md) |
| Web UI changes or UI policy review | [lintapple](.agents/skills/lintapple/SKILL.md), alongside UI guidance |
| Test planning or test-suite pruning | [e2e-first-testing](.agents/skills/e2e-first-testing/SKILL.md) |
| Workflow, lifecycle, retries, or cancellation | [design-explicit-state-machines](.agents/skills/design-explicit-state-machines/SKILL.md) |
| Application-wide workflow discovery and conversion | [make-state-machines-explicit](.agents/skills/make-state-machines-explicit/SKILL.md) |
| Explanations, reports, or updates | [write-clearly](.agents/skills/write-clearly/SKILL.md) |
| Interface wording | [clean-copy](.agents/skills/clean-copy/SKILL.md), alongside writing guidance |
| Pull request descriptions | [pr-description](.agents/skills/pr-description/SKILL.md) |
| PR screenshots, videos, or captions | [pr-visual-evidence](.agents/skills/pr-visual-evidence/SKILL.md) |

Reuse existing code and tools. Verify the changed behavior and run project-required checks. Report completed checks and material gaps accurately; local checks, CI, merge, deployment, and live verification are separate results.
