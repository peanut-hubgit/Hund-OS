# Roadmap

This roadmap orders work by risk and dependency, not by visual feature count.

## Phase 0 — Architecture foundation (current)

- [x] Repository boundaries and initial documentation.
- [x] Draft manifest and schema.
- [x] Security assumptions and threat model.
- [ ] Review architecture decisions with maintainers.

## Phase 1 — Specification and validation

- [ ] Finalize Sub-OS manifest v0.1.
- [ ] Define Hund Language v0.1 grammar.
- [ ] Define VM instruction set or select an existing portable format.
- [ ] Define lifecycle and capability contracts.
- [ ] Build a manifest validator and conformance fixtures.

## Phase 2 — Minimal runtime

- [ ] Implement Sub-OS manager.
- [ ] Implement lifecycle state machine.
- [ ] Implement bounded in-memory virtual filesystem.
- [ ] Execute a minimal non-privileged workload.
- [ ] Add cancellation and resource accounting.

## Phase 3 — Host abstraction

- [ ] Implement host-independent HAL interfaces.
- [ ] Add initial Android adapter.
- [ ] Add Windows adapter.
- [ ] Add Linux adapter.
- [ ] Add capability approval and revocation flows.

## Phase 4 — Language and developer tooling

- [ ] Implement parser and semantic validation.
- [ ] Add formatter and CLI validation tool.
- [ ] Add project templates and diagnostics.
- [ ] Add conformance tests across platforms.

## Phase 5 — Registries and packages

- [ ] Implement local Version Registry.
- [ ] Implement Device Registry with privacy-preserving metadata.
- [ ] Define package format and dependency resolution.
- [ ] Define signing and update trust policy.

## Phase 6 — Hardened execution

- [ ] Threat-model review.
- [ ] Independent security assessment.
- [ ] Platform-specific isolation review.
- [ ] Fuzz parsers and boundary APIs.
- [ ] Define release and support policy.
