---
name: kotlin-as-daredev
description: "Write, refactor, or review Kotlin code using Daredev's personal conventions for Kotlin style, file organization, and domain modeling. Use when working on Kotlin code or when the user asks to apply or extend these Kotlin conventions."
---

# Kotlin as Daredev

Apply these preferences when writing or changing Kotlin code. First load and follow `code-as-daredev` for language-agnostic defaults, Boolean naming, constants, control-flow guards, blank-line grouping, comments, lean tests, and how to apply or extend conventions. This skill adds Kotlin-specific rules on top.

They are personal conventions, not a mandate to rewrite unrelated code. Preserve behavior and follow explicit user instructions; check the surrounding code and build constraints before applying a rule. If a preference conflicts with a required API, language restriction, or project convention, point out the conflict rather than silently breaking the code.

## Load specialized references only when needed

- Read [references/design.md](references/design.md) when designing, adding, refactoring, or reviewing domain models, application boundaries, DTOs, factories, conversions, or type variants.
- Read [references/error-handling.md](references/error-handling.md) when adding, changing, translating, catching, or reviewing error handling, including validation contracts and coroutine cancellation.
- Read [references/testing.md](references/testing.md) when creating, changing, or reviewing Kotlin tests that use testing or mocking tools already available in the project.
- Read [references/project-setup.md](references/project-setup.md) only when creating a Kotlin project, explicitly choosing or replacing test/mock tooling, or selecting tooling where none is established. Do not read it during ordinary work in an existing project.

## Kotlin style and file organization

### Imports

- Import types and use their simple names in code instead of inline fully qualified names. This applies to Java, third-party, and project types.
- When type names collide, use import aliases to keep references unambiguous.
- Import a constant or enum entry directly when its fully qualified use would otherwise make the code noisy. For example, import `Order.Status.COMPLETED` and use `COMPLETED`.
- If two constants or enum entries used in the same file have the same name, import their *distinguishing parent types* instead and qualify each entry with its parent, e.g. `OrderStatus.COMPLETED` and `PaymentStatus.COMPLETED`. If the immediate parent names also collide, use the shortest unambiguous qualification (or an import alias where appropriate).
- Do not shorten names at the expense of clarity or introduce ambiguous imports.

### Naming and calls

- Treat parameter names as a continuation of the function name. When they express the remaining meaning clearly, avoid repeating that meaning in the function name.
- Prefer `findBy(playerId: PlayerId)` over `findByPlayerId(playerId: PlayerId)`, and `createFrom(something: Something)` over `createFromSomething(something: Something)`. This preference applies broadly, not only to lookups.
- Keep a more explicit name when needed for clarity or required by a framework or API.
- Boolean naming follows `code-as-daredev`.
- Use named arguments when a positional argument would obscure its meaning, especially Boolean flags, numeric literals, and adjacent parameters of the same type.
- Do not require named arguments when the meaning is already obvious.

### Functions and control flow

- When convenience overloads provide the same operation for different input forms, delegate to one canonical implementation rather than duplicating logic.
- Add overloads only when useful, and ensure conversions preserve the intended ordering and duplicate semantics.
- Prefer expression bodies (`fun ... = ...`) when a function is a single clear expression.
- Use block bodies when local variables, branching, or multiple steps make the logic easier to follow.
- Do not compress complex logic merely to avoid a block body.
- Guard clauses, early exits, and not replacing errors with silent returns follow `code-as-daredev`.
- Use `?: return` when absence is an expected outcome.
- Use `?: throw ...` when absence is an error, following the project's error-handling conventions.
- Prefer collection operations that directly express the question being asked: `any` for existence, `none` for absence, and `all` for every element matching.
- Avoid filtering or counting merely to check whether a match exists, e.g. prefer `cards.any { it.name == SHELL }` over `cards.filter { it.name == SHELL }.isNotEmpty()`.
- Use implicit `it` for short, obvious lambdas.
- Give parameters descriptive names when lambdas are nested, involve multiple concepts, or make the meaning of `it` unclear.
- Use `also` for a small, closely related side effect, such as logging, when the expression should retain its original result.
- Prefer separate statements when the side effect becomes substantial or obscures execution order.
- Remember that `also` returns its receiver, not the lambda's result.

### Default values

- Follow `code-as-daredev` for default-value rules. Test fixture defaults follow [references/testing.md](references/testing.md).

### Organization and visibility

- Blank-line grouping follows `code-as-daredev`.
- Within classes, keep related declarations together and separate groups with different responsibilities.
- Keep small, closely related declarations together in a descriptively named file when that improves navigation. Do not require one file per class.
- Split declarations when they become large or represent independent concerns.
- When a private helper primarily operates on one object, prefer an extension receiver over passing that object as an ordinary parameter. Keep other inputs as parameters.
- For receiver-style helpers, follow the same placement rule: file-private when independent of class state, class-local when instance dependencies are needed.
- When a private class function does not rely on instance or companion state, move it outside the class as a `private` top-level function at the bottom of the Kotlin file. Update call sites as needed.
- Keep a function in the class when moving it would change semantics or require exposing class internals. Do not move overrides or functions whose placement is required by an interface, framework, or API.
- Prefer a private top-level logger rather than a logger property inside the class. This is the current preference even where older code uses class-local loggers.
- Keep a logger class-local when it genuinely requires instance-specific configuration or context. Preserve the intended logging category when moving it.
- In a module that is not shared with other modules, avoid `internal`; use `public` (or Kotlin's default public visibility) and `private` as applicable.
- Check whether the module is shared before changing existing `internal` declarations. Do not guess from a single file.

### Constants

- Naming, units, and not extracting obvious literals follow `code-as-daredev`.
- If constants are used outside this file and belong to a class, put them in that class's `companion object`.
- If all constants are file-private and no companion object is needed for another reason, declare them as `private` top-level constants near the top of the file (after imports). Do not create a companion object only to hold private constants.
- If the class has a companion object for publicly used, class-related constants, keep its private constants there too rather than splitting the constants between the companion and the file top level.
- Use `const val` only where Kotlin permits compile-time constants; otherwise use `val` with appropriate visibility. Do not move constants in a way that changes initialization behavior or a required API.

## Applying and extending these conventions

Follow `code-as-daredev` for applying and extending conventions. In addition:

1. Inspect existing imports, usages, class state, module boundaries, and constant consumers before editing.
2. When resuming convention discovery, put new Kotlin-specific rules in a conditional reference where appropriate.
3. Do not automatically reintroduce rejected proposals: verifying both positive and absent side effects in tests; preferring copy-based state transformations; returning empty collections rather than null; exhaustive `when` without `else`; structured logging as a general preference; or separate classes for independently selectable rules or strategies.
4. When the user adds or corrects a Kotlin-specific convention, update this skill's rules and examples without inventing additional preferences.
