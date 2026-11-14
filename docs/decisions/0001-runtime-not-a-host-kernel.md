# ADR 0001: Hund OS is initially a hosted runtime

- Status: Accepted as initial direction
- Date: 2026-11-14

## Context

The initial goal is to let Sub-OS environments run inside Android, Windows and other existing systems. Replacing host kernels or booting directly on hardware would multiply hardware, driver, boot and security requirements before the core model is validated.

## Decision

Hund OS starts as a hosted runtime. The Hund Kernel is a logical policy/lifecycle core within that runtime, not a new physical machine kernel in the first milestones.

## Consequences

- The host OS remains responsible for drivers and process isolation.
- HAL adapters provide controlled access to host features.
- A future bare-metal direction would require a separate architecture decision and substantial redesign.
