# Server state and API calls

## Tooling preference

- Prefer TanStack Query (React Query) for managing server state in React. Use queries for reads and mutations for writes.
- TanStack Query complements the API client; it does not replace transport tools such as `fetch` or Axios. Keep transport details in the project's API layer.
- Reuse TanStack Query where it is installed. Follow the installed version and the project's existing integration rather than assuming a particular API version.
- For new projects, prefer it unless the framework provides a more appropriate mechanism.
- In existing projects without it, propose adoption rather than silently adding the dependency or migrating unrelated code.

## Integration and boundaries

- Expose cohesive feature hooks when useful, following the React reference's hook boundaries: return state, data, and actions, not JSX.
- Follow existing query-key and cache-invalidation conventions.
- Apply this preference to server state, not indiscriminately to every API call. Downloads, streaming connections, and server-side framework fetching may need a different mechanism.
