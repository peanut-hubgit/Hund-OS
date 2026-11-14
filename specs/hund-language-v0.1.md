# Hund Language v0.1 (Exploratory Draft)

## Direction

The first Hund Language release is declarative. It describes Sub-OS metadata and a small set of lifecycle hooks. It must not permit raw host calls, reflection or unrestricted native execution.

## Illustrative syntax

```hund
subos "hello" {
  on_start {
    log("Hello from Hund OS")
  }
}
```

This syntax is illustrative and is not yet accepted by an implemented parser.

## Initial language requirements

- Explicit language version.
- Deterministic parsing and bounded nesting.
- Typed values and structured errors.
- No implicit filesystem or network access.
- Host interaction only through capability-checked standard library functions.
- Cancellation and resource accounting at runtime boundaries.

The grammar, type system and bytecode mapping remain open design work.
