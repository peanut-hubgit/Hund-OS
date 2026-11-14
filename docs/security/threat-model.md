# Security Threat Model (Draft)

## Scope

This draft considers a Hund runtime embedded in an existing host OS. It does not claim to provide hypervisor-grade isolation. The host OS and its security mechanisms remain part of the trusted computing base.

## Assets

- Host files and user data.
- Network access and credentials.
- Device and sensor data.
- Runtime integrity and package contents.
- Sub-OS state and inter-instance boundaries.
- User-granted capabilities.

## Threat actors

- A malicious or compromised Sub-OS package.
- A compromised dependency or update source.
- An application attempting to escape its namespace.
- A confused-deputy attack against a privileged host adapter.
- A local attacker with control of the host account.

## Main risks and mitigations

| Risk | Initial mitigation |
|---|---|
| Path traversal | Canonicalize paths and enforce namespace roots after resolution |
| Capability escalation | Deny by default; validate every host call |
| Resource exhaustion | CPU, memory, file and execution quotas; cancellation |
| Malformed manifests | Strict schemas, bounded input size and parser limits |
| Malicious packages | Integrity checks; signed packages before remote distribution |
| Cross-instance leakage | Separate namespaces, scoped handles and tests |
| Secret leakage | Redaction, secure host storage and no secrets in logs |
| Unsafe native extension | No native plugin loading in the initial milestone |

## Security requirements

- The VM must not expose arbitrary reflection or host object access.
- HAL handles must be opaque and scoped to an instance.
- Permission approval must identify the capability, scope and reason.
- Revocation must prevent future calls and trigger cleanup where applicable.
- Resource limits must be enforced by the runtime, not merely declared by the manifest.
- Error messages and logs must not disclose credential contents.

## Known limitations

A process-local interpreter is not a strong sandbox against memory-safety defects in its own implementation. A production release needs a dedicated security review and may require OS process isolation, platform sandbox APIs or a separate service.
