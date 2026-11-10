# GMH public skills

Ten personal engineering skills for design, UI, testing, workflows, writing, and pull requests. See [AGENTS.md](AGENTS.md) for when to use each skill. Cloned third-party skills and plugin bundles are excluded.

## Install with an agent

Give your agent this instruction:

> Download all skills from https://github.com/gholtzap/gmh-public-skills. Read its README and install them for this project. Preserve existing instructions and skills, and report any conflicts.

The agent should:

1. Clone or download this repository to a temporary directory.
2. Copy the complete folders from `.agents/skills/` into the target project's `.agents/skills/`. Keep references and `agents/openai.yaml` files. Skip identical existing folders; report differing folders instead of overwriting them.
3. Merge the routing guidance from this repository's `AGENTS.md` into the project's `AGENTS.md`. Preserve existing instructions and avoid duplicate entries. Its relative links work with the layout above.
4. Confirm that all ten `SKILL.md` files and their local references are present. Report missing tools or unresolved conflicts. Reload the agent session if the new skills are not discovered.

For another agent with a different skill directory, use its supported location and adjust the routing links. Installation does not require changing the application's code or installing every tool mentioned by a skill.

## Requirements

Most skills are instructions only. The Lintapple skill needs the project's Lintapple setup to run its checks; this repository does not bundle that tool. UI work uses the project's existing components first. Missing tools or access must be reported as verification gaps.

## Edit

Edit the relevant `SKILL.md` or supporting reference. Keep the routing links valid and include complete skill folders when sharing updates.
