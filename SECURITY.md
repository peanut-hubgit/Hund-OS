# Security Policy

Hund OS is an early-stage architecture project. It is **not currently a secure sandbox** and must not be used to execute untrusted code or protect sensitive workloads.

## Reporting

Do not publish exploitable details in public issues. Until a private security reporting channel is configured, contact the repository maintainers through their GitHub profile and provide a concise report.

## Security principles

- Host APIs are inaccessible unless exposed through an approved capability.
- Capability grants are scoped to a Sub-OS instance and should be revocable.
- Inputs crossing the host/runtime boundary must be validated.
- Package and runtime artifacts should be integrity-checked.
- Logs must not contain secrets or raw credential material.

See [the threat model](docs/security/threat-model.md).
