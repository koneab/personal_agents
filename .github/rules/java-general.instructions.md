---
description: Core Java language rules (Effective Java, Google Java Style) for all Java sources.
applyTo: '**/*.java'
---

## Style
- Follow the project's Checkstyle configuration; where it is silent, follow the Google Java Style Guide.
- One top-level type per file; no wildcard imports; no unused imports.
- Declare variables in the narrowest scope; use `var` only when the type is obvious from the right-hand side.
- Prefer `final` fields; make classes immutable unless mutation is required.

## Design
- Program to interfaces for collaborators; use concrete types for value objects.
- Prefer composition over inheritance; keep classes `final` unless designed for extension.
- Use static factory methods or builders when a constructor takes more than three parameters.
- Use `record` for immutable data carriers when the declared Java version supports it.
- Use `enum` instead of `int` or `String` constants; use `switch` expressions over `if` chains on enums when supported.
- Keep methods short, single-purpose and at one level of abstraction.

## Null and optionals
- Never return `null` from a method returning a collection, array or `Optional`; return empty instead.
- Use `Optional` only as a return type; never as a field, parameter or collection element.
- Never call `Optional.get()` without a presence check; use `orElseThrow` with a specific exception.
- Validate non-null contracts with `Objects.requireNonNull` in constructors of non-framework classes.

## Collections and streams
- Return unmodifiable collections (`List.of`, `Collections.unmodifiableList`, `stream.toList()`) from public APIs.
- Declare variables with interface types (`List`, `Map`), not implementations.
- Use streams for transformations; use plain loops when side effects or early exits dominate.
- No side effects inside stream lambdas; no `parallelStream()` without measured need.

## Exceptions
- Throw specific, meaningful exceptions; never throw or catch `Throwable`, `Error` or bare `Exception` unless at a boundary.
- Catch the narrowest type; never leave a `catch` block empty.
- Preserve the cause when wrapping: `new DomainException("message", cause)`.
- Use unchecked exceptions for programming errors and unrecoverable states; checked only when the caller can recover.
- Use try-with-resources for every `AutoCloseable`.

## Equality and common contracts
- Override `equals` and `hashCode` together, or not at all; use `Objects.equals` / `Objects.hash`.
- Compare strings and boxed values with `equals`, never `==`.
- Use `BigDecimal` (with explicit scale and rounding) for money, never `double`.
- Use `java.time` types; never `Date`, `Calendar` or `SimpleDateFormat`.
- Inject a `Clock` instead of calling `Instant.now()` / `LocalDate.now()` in business logic.

## Concurrency
- Prefer immutability and thread confinement over locking.
- Use `java.util.concurrent` utilities over `synchronized`, `wait` and `notify`.
- Never share mutable state in singletons (Spring beans are singletons by default).
- Never swallow `InterruptedException`; restore the interrupt flag or propagate it.

## Logging
- Use SLF4J with parameterised messages: `log.info("Order {} created", orderId)`.
- Never use `System.out`, `System.err` or `printStackTrace`.
- Log an exception once, at the boundary that handles it; never log and rethrow.
- Never log secrets, tokens, credentials or personal data.
