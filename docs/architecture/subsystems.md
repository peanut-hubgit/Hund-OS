# Subsystem Responsibilities

| Subsystem | Owns | Must not own |
|---|---|---|
| Hund Kernel | Lifecycle, policy decisions, event bus, quotas | Platform-specific API calls |
| Hund Language | Grammar, parser contracts, semantic validation | Runtime host access |
| Hund VM | Bytecode validation and execution | Device discovery or user consent |
| Runtime | Instance orchestration and service composition | Business logic of host adapters |
| HAL | Host API translation | Permission policy decisions |
| Version Registry | Compatibility metadata | Artifact execution |
| Device Registry | Normalized host capability metadata | Unrestricted hardware identifiers |
| Package Manager | Package metadata, integrity and dependency resolution | Silent privilege escalation |
| Security | Capability definitions, policy evaluation and audit contract | Implicit grants |
| Developer Tools | Project scaffolding, validation and diagnostics | Bypassing runtime validation |

## Suggested implementation language boundaries

The architecture does not mandate one implementation language. A practical first implementation may use Kotlin/JVM for Android-facing runtime components and a portable core in Kotlin or Rust. Native execution and cross-platform packaging should be decided only after a working interpreter and HAL contracts exist.
