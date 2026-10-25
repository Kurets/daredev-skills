# daredev-skills

Offloading bits of my brain into agent skills.

My coding preferences and ways of working, written down so I don't have to keep repeating myself. These are opinionated
conventions, not universal best practices. Take what fits, adapt the rest.

## Skills

| Skill                                                      | What it covers                                                                             |
|------------------------------------------------------------|--------------------------------------------------------------------------------------------|
| [kotlin-as-daredev](skills/kotlin-as-daredev/SKILL.md)     | Kotlin style, domain modeling, error handling, testing, and project setup.                 |
| [frontend-as-daredev](skills/frontend-as-daredev/SKILL.md) | React components and hooks, TypeScript, CSS Modules, and server state with TanStack Query. |
| [commit-as-daredev](skills/commit-as-daredev/SKILL.md) | Concise commit messages, prefixed with a task ID only when available. |

The coding skills keep specialized guidance in references that agents read only when relevant.

## Install

Use the [Skills CLI](https://github.com/vercel-labs/skills) to choose skills and target agents:

```bash
npx skills add kurets/daredev-skills
```

Or select one skill:

```bash
npx skills add kurets/daredev-skills --skill kotlin-as-daredev
npx skills add kurets/daredev-skills --skill frontend-as-daredev
npx skills add kurets/daredev-skills --skill commit-as-daredev
```

Installation is project-local by default. Add `-g` to make a skill available across projects, or `-a claude-code` /
`-a codex` to select an agent explicitly.

To browse without installing:

```bash
npx skills add kurets/daredev-skills --list
```

## Use

Ask your agent to use the installed skill when writing, refactoring, or reviewing the relevant code, or when preparing a commit message. Automatic discovery
depends on the agent; installation alone does not guarantee it will apply a skill on every task.

For consistent use, add a short instruction to your project's agent instructions (`AGENTS.md`, `CLAUDE.md`, or the
equivalent supported by your agent):

```text
Before writing a commit message or creating a commit, load and follow commit-as-daredev.
Before writing or changing Kotlin code, load and follow kotlin-as-daredev.
Before writing or changing React, frontend TypeScript, or CSS code, load and follow frontend-as-daredev.
If a skill is unavailable, say so rather than assuming its rules.
```

Keep project-specific architecture, commands, and exceptions in the project's instructions rather than in these reusable
skills.

## Updates

```bash
npx skills check
npx skills update
```

## Uninstall

Choose globally installed skills to remove interactively:

```bash
npx skills remove -g
```

Or remove a specific global skill:

```bash
npx skills remove kotlin-as-daredev -g
```

Omit `-g` to remove project-local installations; run the command from that project.
Remove any instructions that require a skill if you no longer intend to use it.

## Feedback

Questions, suggestions, and disagreements are welcome in [issues](https://github.com/kurets/daredev-skills/issues).
Please include an example when proposing a change. The goal is to capture my preferences accurately, not collect every
possible best practice.

## License

[MIT](LICENSE)
