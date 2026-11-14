# Hund OS

**Hund OS** is an extensible host-independent runtime and operating-system environment designed to let developers build and run isolated Sub-OS environments on top of existing platforms such as Android, Windows and Linux.

> Status: **architecture foundation / early design**. This repository currently defines boundaries, contracts and implementation milestones. It does not yet contain a bootable operating system or production-ready isolation boundary.

## Vision

Hund OS provides a stable core composed of:

- **Hund Kernel** — lifecycle, scheduling, resource accounting and system services.
- **Hund Language** — a declarative language for describing Sub-OS environments and applications.
- **Hund VM** — a portable execution environment for validated Hund programs.
- **Host Abstraction Layer (HAL)** — platform adapters for Android, Windows and Linux.
- **Version Registry** — compatibility metadata for runtime, language, packages and Sub-OS manifests.
- **Device Registry** — normalized capabilities and identity metadata for host devices.
- **Security model** — capability-based permissions, isolated workspaces and explicit host access.

## Repository layout

```text
Hund-OS/
├── docs/                 # Architecture, specifications and decisions
├── examples/             # Sample Sub-OS manifests and applications
├── schemas/              # Machine-readable manifest and package schemas
├── specs/                # Normative language and runtime specifications
├── tools/                # Developer tooling and validation utilities
├── runtime/              # Runtime and VM implementation
├── kernel/               # Kernel services and scheduling contracts
├── language/             # Hund Language grammar, parser and compiler
├── hal/                  # Host platform abstraction and adapters
├── registry/             # Version, package and device registries
├── security/             # Threat model, permissions and policy contracts
├── tests/                # Cross-component and conformance tests
└── .github/workflows/    # CI validation
```

See [docs/architecture/overview.md](docs/architecture/overview.md) for the system boundaries and [docs/roadmap.md](docs/roadmap.md) for implementation phases.

## Design principles

1. **Host-independent core:** platform-specific APIs stay behind HAL interfaces.
2. **Explicit capabilities:** a Sub-OS receives only the permissions granted to it.
3. **Portable definitions:** manifests describe intent, not host-specific implementation details.
4. **Versioned contracts:** runtime, language, manifest and package compatibility are explicit.
5. **Safe by default:** deny host access unless a capability is declared and approved.
6. **Incremental delivery:** the first milestone validates manifests and runs a small portable workload before advanced isolation or device integration is attempted.

## Current implementation status

| Component | Status |
|---|---|
| Architecture and subsystem boundaries | Initial specification |
| Manifest schema | Draft |
| Hund Language grammar | Draft |
| Kernel interfaces | Draft |
| VM and runtime | Not implemented |
| Android / Windows / Linux HAL | Not implemented |
| Registries | Contract design |
| Production-grade isolation | Not implemented |

## Getting started

At this stage, start with the documentation and sample manifest:

1. Read [the architecture overview](docs/architecture/overview.md).
2. Read [the security model](docs/security/threat-model.md).
3. Inspect [the example Sub-OS manifest](examples/minimal-subos/hund.yaml).
4. Follow the [roadmap](docs/roadmap.md).

No executable runtime is published yet. Commands and APIs described in specifications are design targets unless explicitly marked as implemented.

## Contributing

Contributions should begin with an issue describing the problem, proposed change and affected subsystem. Architecture changes should include or update an Architecture Decision Record in `docs/decisions/`.

## License

The project license has not been selected yet. Until a license is added, all rights are reserved by the copyright holder.
