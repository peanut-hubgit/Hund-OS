# Hund OS Architecture Overview

## 1. Purpose

Hund OS is a portable runtime architecture for creating **Sub-OS environments** that execute within a host operating system. It is not initially intended to replace the host kernel or boot directly on hardware. The host remains responsible for physical device drivers, process isolation and system-level security.

A Sub-OS is a managed environment with its own manifest, filesystem namespace, application lifecycle, permissions, runtime version and declared device capabilities.

## 2. High-level model

```text
+--------------------------------------------------------------+
|                         Host OS                              |
|                 Android / Windows / Linux                    |
+-----------------------------+--------------------------------+
                              |
+-----------------------------v--------------------------------+
|                    Host Abstraction Layer                    |
|       Files | Process | Network | Device | Clock | UI        |
+-----------------------------+--------------------------------+
                              |
+-----------------------------v--------------------------------+
|                       Hund Runtime                           |
|  Sub-OS Manager | VM | Scheduler | Resource Manager | IPC     |
+-----------------------------+--------------------------------+
                              |
+-----------------------------v--------------------------------+
|                        Hund Kernel                           |
| Lifecycle | Capabilities | Events | Services | Accounting    |
+-----------------------------+--------------------------------+
                              |
+-----------------------------v--------------------------------+
|                  Sub-OS instances and apps                   |
|     Manifest | Packages | Virtual FS | App processes         |
+--------------------------------------------------------------+
```

The diagram is logical, not a claim that each box is a separate OS process.

## 3. Core subsystems

### Hund Kernel

The Hund Kernel is the policy and lifecycle core inside the runtime process. It owns Sub-OS creation, state transitions, resource quotas, service discovery, event routing and capability checks. It does not directly drive hardware.

### Hund Language

Hund Language describes Sub-OS configuration and, in later phases, application behavior. Its first version should be declarative and deliberately small. It must not expose arbitrary host calls or unrestricted native code.

### Hund VM

The VM executes validated, portable bytecode or another explicitly versioned intermediate representation. The VM must provide deterministic validation, bounded memory, cancellation points and host-call mediation. The bytecode format remains a specification target until implemented.

### Host Abstraction Layer (HAL)

HAL provides narrow interfaces for host features. Initial interfaces should include storage, clock, logging and app lifecycle. Network, process, notifications, sensors and graphics can be added later behind separate capabilities.

Each platform adapter translates an interface into host APIs. No core subsystem should import Android, Win32 or Linux-specific APIs directly.

### Version Registry

The Version Registry records compatibility among:
- Hund runtime versions;
- Hund Language and bytecode versions;
- manifest schema versions;
- package format versions;
- HAL contract versions.

Compatibility must be checked before a Sub-OS is started. A registry entry is metadata, not executable code.

### Device Registry

The Device Registry exposes a normalized, privacy-conscious view of host capabilities. It should report only properties needed by a Sub-OS, such as available memory class, supported feature identifiers and display capabilities. Stable hardware identifiers must not be exposed by default.

### Sub-OS Manager

The manager validates manifests, resolves dependencies, creates isolated namespaces, requests declared capabilities, starts and stops instances, and records instance state.

### Package Manager

The package manager installs and removes signed or integrity-verified packages, resolves dependencies and checks compatibility. Trust policy and signature verification must be defined before remote package installation is enabled.

## 4. Dependency direction

- Domain contracts must not depend on platform adapters.
- Kernel and VM depend on interfaces, not Android/Windows/Linux classes.
- HAL adapters implement contracts defined by the core.
- User interfaces and developer tools communicate with the runtime through a versioned control API.
- Registries are consumed through interfaces so the initial implementation can use local files before a remote service exists.

## 5. Lifecycle

A Sub-OS instance follows this conceptual state machine:

`CREATED -> VALIDATING -> RESOLVING -> WAITING_FOR_PERMISSIONS -> STARTING -> RUNNING -> STOPPING -> STOPPED`

Any pre-running state may transition to `FAILED`. A running instance may transition to `SUSPENDED` and back to `RUNNING` when the host supports it. Every transition must be observable and auditable.

## 6. Initial implementation boundary

The first working milestone should:
1. Parse and validate a local YAML/JSON manifest.
2. Check schema and runtime compatibility.
3. Create a virtual in-memory filesystem namespace.
4. Start a minimal, non-privileged workload in a bounded interpreter.
5. Stop the workload and release resources.
6. Produce structured lifecycle events.

Do not begin with arbitrary shell execution, native plugin loading, unrestricted networking or direct device access.

## 7. Non-goals for the first release

- Replacing Android, Windows or Linux kernels.
- Booting on bare metal.
- Running arbitrary APK, EXE or ELF binaries.
- Providing a security boundary equivalent to a hypervisor or hardware-backed virtual machine.
- Exposing all host APIs to Sub-OS applications.
