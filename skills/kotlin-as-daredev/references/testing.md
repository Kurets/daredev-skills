# Testing with established tools

Read this reference when creating, changing, or reviewing Kotlin tests that use testing or mocking tools already available in the project. Do not use it to select, add, or replace test or mocking frameworks.

## Kotest

- When Kotest is available, prefer `ShouldSpec`, using `context` to group related scenarios and `should` to describe expected behavior.
- Otherwise, use the project's existing test framework. Follow the existing suite's style when extending tests; do not add Kotest or migrate existing tests solely to apply this preference.
- Prefer Kotest's infix assertion syntax when readable, e.g. `actual shouldBe expected` rather than `actual.shouldBe(expected)`.

## MockK

- Use MockK when already available; otherwise respect the project's existing library rather than introducing another solely for this preference.
- Prefer non-relaxed MockK mocks with explicit stubbing for dependencies whose behavior matters to the test.
- Use relaxed mocks selectively for incidental collaborators, rather than enabling relaxation across the suite.

## Fixtures

- For complex or repeatedly constructed test objects, prefer reusable fixture factories or Kotlin builder DSLs with valid defaults.
- Keep scenario-relevant values explicit in each test.
- Allow randomized fixture defaults for incidental values, such as IDs or names, while explicitly setting values that affect the behavior under test. Do not let random defaults decide whether a test passes or fails.
- Reuse existing builders before adding new ones; use direct constructors for simple cases.
