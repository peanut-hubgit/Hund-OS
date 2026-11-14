# ADR 0002: Capability-based host access

- Status: Accepted as initial direction
- Date: 2026-11-14

## Context

Sub-OS programs may need storage, networking or device functions. Direct unrestricted host access would undermine portability and security.

## Decision

Host features are exposed through named capabilities. Capabilities are declared in a manifest, evaluated by policy and approved where required. Runtime host calls are checked against the instance's effective grants.

## Consequences

- Access is denied by default.
- Capabilities have explicit scopes and lifecycle.
- New host features require contract and security review.
