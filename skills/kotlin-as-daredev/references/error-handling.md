# Error handling

Read this reference when adding, changing, translating, catching, or reviewing error handling, including validation contracts and coroutine cancellation.

## Invalid arguments, invalid state, and business failures

- Use `require` / `requireNotNull` when an argument violates the function's input contract, e.g. `require(amount > 0) { "Amount must be positive" }`. These throw `IllegalArgumentException`.
- Use `check` / `checkNotNull` when the object's or system's current state prevents an operation, e.g. `check(status == WAITING) { "Game has already started" }`. These throw `IllegalStateException`.
- Use a specific domain exception when callers need to distinguish a business failure, such as `InsufficientFunds`, following project conventions.
- `requireNotNull` and `checkNotNull` apply the same distinction to null values and return the non-null value.

## Catching exceptions

- Prefer catching specific exception types that the code can meaningfully handle or translate.
- Avoid catching `Throwable` for ordinary application failures.
- In coroutine code, propagate cancellation rather than swallowing it or translating it into a business error.

## Translating exceptions

- When translating a lower-level exception into an application or domain exception, preserve the original exception as its cause.
- Add meaningful context without exposing credentials or other sensitive data.
- Do not replace the original failure with only its message.
