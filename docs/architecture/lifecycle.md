# Sub-OS Lifecycle

## States

- `CREATED`: manifest accepted as input, not yet trusted.
- `VALIDATING`: syntax, schema and semantic checks are running.
- `RESOLVING`: runtime, package and capability dependencies are resolved.
- `WAITING_FOR_PERMISSIONS`: user or administrator approval is required.
- `STARTING`: namespaces and runtime resources are prepared.
- `RUNNING`: workload can execute within granted limits.
- `SUSPENDED`: execution is paused while state is retained.
- `STOPPING`: cancellation and cleanup are in progress.
- `STOPPED`: resources have been released.
- `FAILED`: startup or execution failed; diagnostics are available.

## Invariants

1. A workload cannot enter `RUNNING` before validation and policy evaluation succeed.
2. A denied capability cannot be used as a fallback to a broader host API.
3. `STOPPED` means all runtime-owned resources have been released or explicitly recorded as failed cleanup.
4. State transitions produce structured events.
5. Cancellation is cooperative inside the VM and enforced by the runtime at host-call boundaries.
