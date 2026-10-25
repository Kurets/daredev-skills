# Maintaining daredev-skills

This file guides agents maintaining this repository. It is not part of the instructions users install with individual skills.

## Scope

- Preserve DareDev's personal conventions. Do not invent preferences or present them as universal best practices.
- Ask before adding, removing, or materially changing a convention. For discovery, propose one candidate at a time with evidence and draft wording. Existing code alone is not approval.
- Keep private paths, credentials, employer-specific details, and other non-public material out of skills, examples, and documentation.

## Structure and loading

- Keep each skill self-contained under `skills/<skill-name>/`, with a `SKILL.md` containing matching `name` and a clear `description` explaining when to use it.
- Keep `SKILL.md` focused. Put specialized guidance in `references/`, using relative links and explicit conditions for when an agent should read or skip each reference.
- Do not require agents to load every reference upfront. Avoid duplicating rules across the entry point, references, and README.
- Keep supporting files within the skill directory; installed skills must not depend on this root file or files in another repository.
- Use the README for human-facing descriptions, installation, and usage. Keep it consistent with the actual skill names and repository layout.
- Do not add categories, plugin packaging, release tooling, or setup workflows without a concrete need and approval.

## Changes and verification

- Make the smallest relevant change. Preserve the meaning and exceptions of approved rules when reorganizing files.
- Check Markdown formatting, code fences, frontmatter names/descriptions, relative links, and referenced file existence after edits.
- Verify copied files against their source when performing a copy-only migration. Do not silently clean up or change conventions during a copy.
- Do not modify installed skill copies or another repository unless explicitly authorized. A copied skill's maintenance workflow is not authorization to synchronize other locations.
- Do not load both coding skills merely to edit this repository's Markdown. Load the relevant skill when the actual task requires its coding conventions.
- Report what was checked and what could not be verified. Do not claim installation commands were tested unless they were run.
