---
name: code-as-daredev
description: "Apply Daredev's language-agnostic coding conventions: defaults, Boolean naming, constants, control-flow guards, shallow nesting via named helpers, blank-line grouping, comments, lean behaviour-focused tests, and how to apply or extend conventions. Use whenever writing, refactoring, reviewing, or testing code in any language, and before loading a language-specific Daredev skill such as kotlin-as-daredev or frontend-as-daredev."
---

# Code as Daredev

Language-agnostic coding preferences. Load this whenever writing, changing, or testing code. Stack-specific skills (for example `kotlin-as-daredev` or `frontend-as-daredev`) add on top of these rules; they do not replace them.

## Default values

- Do not give a parameter, option, property, or prop a default value when it selects behavior (mode, flag, strategy, limit, timeout, or anything that changes branching, validation, or persistence). Make it required so each caller chooses explicitly.
- Defaults are fine for incidental values that cannot change behavior (e.g. optional metadata). When absence is allowed, prefer an optional/nullable form over an invented placeholder (`displayName?: string` / `displayName: String? = null`, not `'Guest'`).
- Do not add a default to a new parameter merely to avoid updating callers; update the callers.
- Keep defaults required by a framework, library, serialization, or public API; point out the conflict instead of removing them silently.
- Apply only to code being written or changed. Do not strip existing defaults from unrelated code.

## Boolean naming

- Name Boolean values and Boolean-returning functions as clear predicates, using prefixes such as `is`, `has`, `can`, or `should` where natural.
- Prefer names that make conditions readable without inspecting the implementation (e.g. `if (game.isFinished)`, `if (player.canAttack(target))`).
- Do not force an unnatural prefix or rename a required external API.

## Constants and literals

- Give meaningful thresholds, limits, timeouts, weights, and repeated protocol or domain values descriptive names instead of embedding unexplained literals in logic.
- Include units or scale in the name when useful (e.g. `TIMEOUT_MS`, `MISTAKE_PERCENTAGE`, `MAX_RETRIES`).
- Do not extract obvious literals merely to eliminate every number or short string (e.g. `0`, `1`, `''`).
- Prefer existing enums, unions, or shared constants when the project already has them; do not invent a parallel constant layer.

## Control flow

- Prefer guard clauses and early exits when they reduce nesting and keep the main flow clear.
- Prefer shallow nesting. When conditionals nest more than about one level, or the happy path is buried, extract cohesive branches into named helpers (or local functions) that themselves use early returns.
- Name those helpers so the call site reads as the decision tree; a reader should understand the flow from the names without diving into every body.
- Do not extract trivial one-liners merely to avoid a single `if`/`else`. Extract when it improves readability of the surrounding flow.
- Preserve execution order, side effects, and error behavior when flattening or extracting branches.
- Do not replace an error with a silent return merely to simplify the code.

## Blank lines and grouping

- Use blank lines to divide code into meaningful, cohesive groups.
- Keep statements together when they contribute to the same immediate purpose, even when they are different kinds of statements.
- Insert a blank line when the purpose or step changes (e.g. preparing inputs → processing → constructing the result).
- Keep a loop or conditional with its directly related setup when they form one logical step. Do not automatically surround every control-flow statement with blank lines.
- Avoid both unbroken walls of statements and a blank line after every statement. Group by meaning, not a fixed number of lines.

## Comments

- Do not add comments that only restate what the code already makes obvious.
- Prefer clarifying names and structure over narrating comments.
- A comment is warranted when it records non-obvious intent, a constraint, a trade-off, or a why that the code itself does not imply.
- Do not leave TODOs, speculative notes, or commented-out code unless I explicitly ask for them.

## Testing

- Test meaningful behaviour a consumer would depend on — what the unit does with its inputs and collaborator states — not exhaustive coverage of every branch or input.
- Keep tests concise. Prefer a clear arrange/act/assert (or equivalent) without unnecessary ceremony, duplication, or setup that does not affect the outcome.
- Do not over-test infrastructure: avoid spinning up app containers, embedded brokers, full framework contexts, or heavy integration harnesses unless I explicitly ask for that kind of test.
- Test through the public API. Do not target private helpers directly or use reflection to reach them.
- Cover critical paths and meaningful edge cases (e.g. null/absence, zero, negative, or alternate branches) when they matter to the behaviour under test — not every combinatorial possibility.
- Follow the project's existing test style and libraries. Do not introduce new testing frameworks or dependencies solely to apply these preferences.

## Applying these conventions

- Personal conventions, not a mandate to rewrite unrelated code. Preserve behavior and follow explicit user instructions.
- If a preference conflicts with a required API, language restriction, or project convention, point out the conflict rather than silently breaking the code.
- Prefer the smallest change that follows the applicable rules; follow the project's formatter; avoid unrelated churn.
- Run available relevant formatting, type checks, compilation, and tests; state what was not run.

## Extending these conventions

- Propose one distinctive convention at a time with evidence and draft wording; existing code is evidence to discuss, not automatic approval.
- Add or change preferences only after confirmation.
- Update this skill on approval; do not invent extra preferences.
- Do not automatically reintroduce declined proposals. Language-specific skills keep their own declined lists.
