# TypeScript and module conventions

Language-agnostic defaults, Boolean naming, constants, and control-flow guards live in `code-as-daredev`. This file keeps TypeScript-specific rules.

## Types and absence

- Prefer `type` over `interface`. Keep an interface when declaration merging or another required contract depends on it.
- Use `undefined` for values not yet defined or omitted. Prefer optional parameters such as `value?: string` when omission is allowed.
- Use `null` to represent intentional absence, including an explicitly empty result such as `findValue(): string | null`.
- Do not mechanically change every `T | undefined` return type to `T | null`: preserve existing API, library, serialization, and state contracts. Follow the meaning of the absence.

## Default values

- Follow `code-as-daredev` for default-value rules.
- Shared design-system components may keep a conventional default, such as a `Button` defaulting to its primary variant.

## Constants and literals

- Naming, units, obvious literals, and reusing existing enums/unions/shared constants follow `code-as-daredev`.
- Do not extract single-use UI copy already handled by localization merely to create a constant.

## Boolean naming

- Follow `code-as-daredev`. Applies to props and Boolean-returning functions as well.

## Control flow

- Guard clauses, early returns, and not replacing errors with silent returns follow `code-as-daredev`. Prefer that shape over `else` when it keeps the happy path clear.
- Keep ternaries short and simple. Do not nest ternaries; avoid multiline branches that obscure the flow. Use a helper with early returns, an intermediate value, or extracted components instead.
- Do not call a `const` helper before its initialization. A helper declared later at module scope is safe when it is only called after module initialization, such as during rendering.

```typescript
const getMessage = (isLoading: boolean, hasError: boolean): string => {
  if (isLoading) return 'Loading';
  if (hasError) return 'Failed';
  return 'Ready';
};

const label = isOpen ? 'Close' : 'Open';
```

## Imports and exports

- Use named exports, not default exports, for your own declarations. Keep default exports where a framework or tool requires them; default imports from third-party APIs are fine.
- Prefer configured absolute or aliased imports across directories. Keep same-folder imports, such as `./example.module.css`, relative.
- Reuse the project's actual aliases; do not invent aliases that its compiler, bundler, and tests cannot resolve. If no suitable alias exists, follow the project's working import setup and flag the limitation. Do not introduce new alias infrastructure without agreement.
