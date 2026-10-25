# Test and mock tooling selection

Read this reference only when creating a Kotlin project, explicitly choosing or replacing test/mock tooling, or selecting tooling where none is established. Do not read it during ordinary work in an existing project, and do not propose adding Kotest, MockK, or migrating frameworks then.

- When setting up a new Kotlin project or choosing a test framework where none is established, prefer Kotest with `ShouldSpec`, subject to project requirements and compatibility.
- When setting up Kotlin tests that need mocking and no mocking library is established, prefer MockK.
