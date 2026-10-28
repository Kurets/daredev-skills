---
name: commit-as-daredev
description: "Write a single-line git commit message using DareDev's conventions: a plain-language description, prefixed with the task ID from the current branch only when one exists. Use when asked to write, generate, or suggest a commit message, or to commit changes."
---

# Commit as DareDev

Write one short commit message for the staged changes, or the changes the user identifies. This skill defines message
conventions; it does not itself authorize creating a commit or pushing it.

## Inspect the change

1. Read the current branch with `git branch --show-current`.
2. Detect a task ID at the start of the branch name, ignoring a leading prefix such as `feature/`, `bugfix/`, or
   `hotfix/`. A task ID consists of uppercase letters, a dash, and digits.
    - `QWE-1234-fix-auth` gives `[QWE-1234]`.
    - `feature/QWE-1234-fix-auth` gives `[QWE-1234]`.
    - `main` or `refactor-cleanup` has no task ID; omit the prefix.
3. Inspect `git diff --staged`. If nothing is staged, inspect `git diff`; inspect relevant untracked files if they are
   part of the requested change. Do not describe unseen changes.
4. Identify the main purpose of the change.

## Task prefix

Prefix the message with `[TASK-ID]` when the branch contains a task ID as described above. Otherwise, start directly
with the description. Do not add placeholder prefixes.

## Message format

```text
# With a task ID:
[TASK-ID] <third-person present-tense verb> <what the change does>

# Without a task ID:
<third-person present-tense verb> <what the change does>
```

- Exactly one line: no body, bullet list, or trailing period, except for explicitly requested co-author trailers.
- Do not add co-authors (including `Co-authored-by` trailers) unless the user explicitly requests them.
- Start the description with a verb such as `Adds`, `Changes`, `Fixes`, `Removes`, `Updates`, `Refactors`, `Improves`,
  `Renames`, `Moves`, `Documents`, or `Tests`.
- Keep it short and focused on the main change. Avoid verbose descriptions or a list of unrelated edits.
- Describe behavior or purpose in plain language, not class, method, or file names.

## Examples

Good:

- `[QWE-1234] Adds retry for failed payment notifications`
- `[QWE-1234] Changes session expiry to use the user's timezone`
- `Adds profile deletion`
- `Prevents duplicate submissions`
- `Improves search result readability`
- `Refactors validation to separate it from rendering`
- `Explains skill installation`
- `Updates development dependencies`

Bad:

- `Fixes PaymentService.send()` — describes an implementation name instead of behavior.
- `QWE-1234 added retry` — missing brackets, wrong verb form, and too vague.
- `[TASKLESS] Adds profile deletion` — adds a placeholder instead of omitting the prefix.
- `Adds search, fixes login and updates dependencies` — lists unrelated changes instead of one main purpose.
