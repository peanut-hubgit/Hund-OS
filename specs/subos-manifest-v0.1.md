# Sub-OS Manifest Specification v0.1 (Draft)

## Purpose

A manifest declares identity, compatibility, resource limits, capabilities and entry point for one Sub-OS package.

## Required fields

- `manifestVersion`: schema version.
- `id`: stable reverse-domain identifier.
- `name`: human-readable name.
- `version`: semantic version.
- `runtime`: accepted Hund runtime version range.
- `entrypoint`: package-relative workload entry point.

## Optional fields

- `description`
- `publisher`
- `languageVersion`
- `resources`
- `capabilities`

## Rules

1. Unknown critical fields must cause validation failure.
2. Paths must be relative and must not escape the package root.
3. Resource limits must be finite and within host policy.
4. Capabilities are requests, not grants.
5. Manifest parsing must enforce document size and nesting limits.
6. This draft does not define executable bytecode semantics.
