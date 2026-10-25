# React conventions

## Components and imports

- Declare components with `const` and arrow functions, typed using the named `FC` type from `react`.
- Import hooks by name and call `useState`, `useEffect`, or `useContext`, not `React.useState`, `React.useEffect`, or `React.useContext`.
- Prefer type-only imports for `FC` when supported by the project's TypeScript configuration. Do not add an unused default React import with the automatic JSX runtime. Keep the runtime import when the classic JSX transform requires it.
- Preserve necessary generic inference or framework-specific component signatures when `FC` cannot express them correctly; explain the exception instead of forcing an unsafe annotation.

```tsx
import type { FC } from 'react';
import { useState } from 'react';

type Props = {
  initialName: string;
};

export const Example: FC<Props> = ({ initialName }) => {
  const [name, setName] = useState(initialName);

  return (
    <button type="button" onClick={() => setName(capitalize(name))}>
      {name}
    </button>
  );
};

const capitalize = (value: string): string =>
  value.charAt(0).toUpperCase() + value.slice(1);
```

## Props naming and destructuring

- Represent mutually exclusive component modes with a named union prop such as `variant` or `size`, rather than Boolean flags that permit contradictory combinations. Keep independent Boolean behaviors as separate props.
- An unexported props type in the component's own file may be called `Props`.
- Give exported props types and props types in separate files a component-specific name, such as `ExampleProps`, not `Props`.
- Destructure props in the parameter list when it fits clearly on one line under the project's formatter.
- If parameter destructuring would span multiple lines, accept `props` and destructure inside the component instead.
- If the internal destructuring also becomes multiline, consider splitting the component, grouping genuinely related props, or accessing some props directly. Do not create meaningless groups or fight the formatter merely to reduce line count.

```tsx
type Props = {
  title: string;
  description: string;
};

export const Example: FC<Props> = ({ title, description }) => (
  <section>
    <h1>{title}</h1>
    <p>{description}</p>
  </section>
);
```

## Helpers and component identity

- Move helpers that do not depend on component scope to module scope, below the main component. Pass their inputs explicitly. Preserve safe initialization order if a helper is needed during module initialization.
- A dependency includes props, state, context, refs, and other render-local values—not only state.
- Keep handlers and closures local when they need component scope; do not force every function outside the component.
- When extracting a React component, define it at module scope and pass props. Do not define a component inside another component and render it as `<NestedComponent />`: its identity changes on every render and can reset state or remount its subtree.
- Distinguish ordinary render helpers called as functions from React component definitions. Helpers must not call hooks; component extraction should preserve behavior rather than hiding closure dependencies.

## Hook and component responsibilities

- Custom hooks expose state, derived data, and actions; keep rendering in components.
- Do not return JSX from hooks. Let the consuming component render the UI explicitly using the hook's returned values.
- Prefer an object with named fields when a hook returns multiple values. Allow tuples for natural value/setter or value/action pairs, such as `[isOpen, toggle]`. A hook that exposes one value can return it directly.
- Expose actions when the hook owns a meaningful operation or coordinates state transitions. Raw setters are fine for simple state utilities. Do not create trivial wrapper functions solely to hide setters.
- Use an options object when a hook has several inputs, optional settings, or positional arguments that would be ambiguous. Keep a single obvious input positional; do not wrap every argument in an object automatically.
- Extract a hook when it represents a cohesive behavior and makes the component easier to understand, even with one consumer. Keep simple local state inline. Avoid moving all component logic into a catch-all hook merely to shorten the component.

## Memoization

- Do not add `useMemo`, `useCallback`, or `memo` routinely. Use them for a concrete performance or reference-identity requirement, and keep their dependencies correct.
- A concrete reason does not necessarily require a benchmark. Do not treat memoization as default boilerplate.

## Callback and handler naming

- Name callback props after the event, such as `onClose`, `onConfirm`, or `onChange`.
- Name local event adapters with `handle…`, such as `handleMouseEnter`.
- Keep meaningful action names such as `deleteAccount` for business operations. Do not rename every function to `handle…` merely because an event triggers it.

## File organization and recursive colocation

- Keep small components and hooks in a single file.
- Treat roughly 250 lines as a signal to reconsider organization, not a hard limit. When a component or hook grows, consider replacing its file with a same-named folder at the same directory level.
- Inside that folder, keep the implementation (`example.tsx` or `useExample.ts`), component- or hook-specific types (`example.types.ts` or `useExample.types.ts`), and an `index.ts` with named exports. Colocate associated styles when applicable. Do not create empty or trivial types files merely to complete the structure.
- Preserve the public import path where possible.
- Keep owner-specific subcomponents and hooks inside the owning component's folder; keep hook-specific helper hooks inside the owning hook's folder.
- Apply the same organization recursively: small children remain single files, while growing children get their own subfolders.
- Move genuinely shared code to the nearest appropriate shared location when multiple independent consumers need it. Do not prematurely promote implementation details into shared abstractions.
- Split by cohesive responsibility rather than merely staying below a line count. Moving types alone is not enough when the implementation itself remains large.

## Conditional rendering

- Return `null` when a component should render nothing, not an empty fragment.
- Keep short ternaries for simple alternatives. Replace nested or substantial JSX ternaries with clear branches or module-scope components.
- Keep hook calls unconditional and before early returns that would otherwise change hook order.
- When replacing complex JSX, preserve the existing event handlers, ordering, keys, and accessibility behavior.

```tsx
import type { FC } from 'react';

type Props = {
  shouldRender: boolean;
  isSelected: boolean;
  label: string;
};

export const Example: FC<Props> = (props) => {
  const { shouldRender, isSelected, label } = props;
  if (!shouldRender) return null;

  return isSelected ? <strong>{label}</strong> : <span>{label}</span>;
};
```
