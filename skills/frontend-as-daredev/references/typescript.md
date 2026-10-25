# TypeScript and module conventions

## Types and absence

- Prefer `type` over `interface`. Keep an interface when declaration merging or another required contract depends on it.
- Use `undefined` for values not yet defined or omitted. Prefer optional parameters such as `value?: string` when omission is allowed.
- Use `null` to represent intentional absence, including an explicitly empty result such as `findValue(): string | null`.
- Do not mechanically change every `T | undefined` return type to `T | null`: preserve existing API, library, serialization, and state contracts. Follow the meaning of the absence.

## Boolean naming

- Name Boolean values, including props, and Boolean-returning functions as readable predicates, using `is`, `has`, `can`, or `should` where natural.
- Prefer names that make conditions understandable without inspecting the implementation. Do not force an unnatural prefix or rename a required external API.

## Control flow

- Avoid `else`; prefer guard clauses and early returns to reduce nesting. Preserve execution order, side effects, and error behavior.
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
