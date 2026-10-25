# Extending these conventions

1. Inspect the project's dependencies, JSX runtime, formatting configuration, aliases, and relevant code before editing.
2. Make the smallest relevant change. Follow the project's formatter rather than copying indentation or quote choices from examples.
3. Run relevant available formatting, type checks, and tests. State what was not run; do not assume a build performs type checking.
4. For convention discovery, inspect actual repository code and propose one distinctive convention at a time with file evidence and draft wording. Existing code is evidence to discuss, not automatic approval.
5. Add or change preferences only after user confirmation. Do not infer choices of state management, testing libraries, localization tooling, design systems, or project structure from their presence in one repository.
6. Update the repository skill on approval. Update an installed copy only when installation or synchronization is authorized; repository-only setup must remain repository-only.
7. Do not reintroduce declined proposals unless the user asks to reconsider: a personal singleton convention; a preference for accessible, user-facing queries in component tests; an explicit button-type convention; preferring derived values over synchronized duplicate state.
