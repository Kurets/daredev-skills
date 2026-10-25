# CSS Modules conventions

Apply this reference only in repositories that use CSS Modules. If the repository uses a different styling approach, skip this reference rather than introducing CSS Modules.

## CSS Modules

- Prefer CSS Modules for component styling, imported as `styles` from a `*.module.css` file.
- Use meaningful component class names.
- Reuse existing design tokens when they express the intended style. Do not duplicate them with hardcoded values or invent tokens for every literal.
- Do not replace the application's required global stylesheet, resets, or third-party integration classes merely to enforce component-local styling.
- Follow existing file naming and CSS tooling. Do not introduce or replace a styling framework without agreement.

```tsx
import type { FC } from 'react';
import styles from './example.module.css';

export const Example: FC = () => (
  <div className={styles.example}>
    <h1>Example</h1>
  </div>
);
```

```css
/* example.module.css */
.example {
    display: flex;
    align-items: center;
    padding-block: 1rem;
}
```

## Class name composition

- Import `classnames` as `cn`, not `classnames`, `evaluateClasses`, or another name.
- Use `cn` for conditional classes or composing multiple classes. Use computed object keys for conditional CSS Module classes.
- Do not wrap a single unconditional class name in `cn`.
- Compose CSS Module classes consistently with the surrounding code.
- Check whether `classnames` is available before importing it. Do not silently add a dependency to enforce this preference.

```tsx
import cn from 'classnames';

// One unconditional class:
<span className={styles.wrapper} />;

// Base and conditional classes:
<button
  type="button"
  className={cn(styles.button, {
    [styles.error]: isError,
    [styles.small]: size === 'small',
  })}
/>;

// Multiple unconditional classes:
<div className={cn(styles.panel, sharedStyles.surface)} />;
```
