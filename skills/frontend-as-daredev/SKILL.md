---
name: frontend-as-daredev
description: "Write, refactor, or review frontend code using Daredev's personal conventions for React, TypeScript, and CSS. Use when working on React components, hooks, frontend TypeScript, or styling, or when asked to apply or extend these conventions."
---

# Frontend as Daredev

Apply these personal preferences without rewriting unrelated code. Preserve behavior, follow explicit user instructions, and inspect project constraints. Point out conflicts with required APIs or tooling rather than breaking them. Older code is not more authoritative than these preferences.

## Load only applicable references

Do not read every reference upfront. Select by the work being performed, not merely by file extension or installed dependencies. Multiple references may apply; skip unrelated ones.

- [references/typescript.md](references/typescript.md): when writing or reviewing frontend TypeScript/JavaScript logic, types, control flow, naming, imports, or exports. Skip for CSS-only work.
- [references/react.md](references/react.md): when writing or reviewing React components, props, hooks, rendering, memoization, or component/hook organization. Skip for styling-only changes.
- [references/server-state.md](references/server-state.md): when writing or reviewing React API integration, server-state queries or mutations, caching, or server-state tooling choices. Do not load merely because TanStack Query is installed.
- [references/styling.md](references/styling.md): when working on styling or class names in a repository that uses CSS Modules. Otherwise, skip it and follow the existing styling approach. Prefer CSS Modules for new projects; do not introduce them into an existing repository that does not use them.
- [references/convention-discovery.md](references/convention-discovery.md): only when discussing, adding, or changing this skill's conventions. Skip during ordinary implementation and code review.

## Localization

When a project has localization, use its existing translation mechanism for user-facing text, including accessibility labels. Update required locale files; do not introduce localization tooling just to enforce this preference.

## Applying the rules

Inspect relevant dependencies, configuration, and surrounding code. Make the smallest relevant change and follow the project's formatter. Run available relevant formatting, type checks, and tests; state what was not run. Do not assume a build performs type checking.
