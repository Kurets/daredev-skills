# Design and domain modeling

Read this reference when designing, adding, refactoring, or reviewing domain models, application boundaries, DTOs, factories, conversions, or type variants. These are design preferences, not requirements imposed by Kotlin or a mandate to introduce DDD into every project.

## Dependency boundaries

- Inject dependencies through constructors.
- At infrastructure boundaries, prefer consumer-facing interfaces so application logic does not depend directly on database, HTTP, or other infrastructure implementations.
- Do not create an interface for every class automatically.

## Interface and implementation naming

- Name interfaces after the capability or role they represent, without implementation details or markers such as `I` or `Interface`.
- Name implementations to explain the technology, strategy, or behavior that distinguishes them, e.g. `GameRoomRepository` → `ExposedGameRoomRepository`, `CardRepository` → `InMemoryCardRepository`, or `TargetsPredictor` → `RandomForestTargetsPredictor`.
- Avoid vague implementation names such as `Impl` or `Default` when a meaningful distinction exists.

## Type-owned factories

- When a factory naturally belongs to one type, prefer a named function in that type's companion object over a standalone factory function or separate factory class.
- Use constructors for straightforward construction; keep factories requiring injected dependencies in the appropriate service or factory.

## Type ownership and DTO placement

- Prefer nesting small supporting types inside their owning type when their meaning belongs specifically to that owner—not only sealed variants. Keep independently useful or substantial types separate.


- Organize request and response DTOs by their owning feature or use case, keeping them near their consumers.
- Avoid a catch-all DTO package that mixes unrelated features.
- Move a type into shared code only when it genuinely has shared ownership or consumers.

## Model and DTO conversions

- Prefer top-level extension functions named `to<Target>()` for straightforward model/DTO conversions, e.g. `fun Player.toPlayerData() = PlayerData(...)`, rather than mapper classes or service methods.
- Keep conversion functions near the relevant models or consumer. Do not force this pattern when mapping needs injected dependencies.

## Named multi-value results

- When a function returns multiple values with distinct domain meanings, prefer a named data class with descriptive properties over `Pair`, `Triple`, or positional collections.
- Use pairs and destructuring for simple local operations where the meaning is clear, such as Kotlin's `partition`.
- Prefer meaningful property access such as `result.allies` over positional access such as `result.second` for domain results.

## Closed sets of variants

- For a closed set of distinct variants with different data or behavior, prefer a sealed interface with dedicated implementations over one class containing flags and nullable variant-specific fields.
- Prefer an enum when variants are simply named values. Use a sealed class when shared state or constructor logic is needed.
- Apply the type-ownership nesting preference to small sealed variants too, e.g. `AuthRequest.Google` rather than a standalone `GoogleAuthRequest`. Keep substantial implementations or independently useful types separate.

## Value objects, type aliases, and validation

- Prefer a value object for a domain “atom”—a meaningful domain concept. Use a `typealias` for helper or supporting types that do not warrant a distinct domain type, or to make a long or unclear underlying type easier to understand. A type alias provides naming, not separate type safety.
- Enforce a value object's intrinsic constraints in its constructor or `init` block using `require` with a descriptive message, so invalid instances cannot be created.
- Keep checks requiring repositories or external state outside the value object.
- Prefer `@JvmInline value class` for a value object wrapping a single value when Kotlin's value-class restrictions and the project's framework, serialization, persistence, and interoperability requirements allow it. Otherwise use an appropriate regular or data class.
- Before converting an existing type to a value class, check its consumers and compatibility requirements; do not assume the change preserves its API or runtime representation.
