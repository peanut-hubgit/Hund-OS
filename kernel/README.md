# Hund Kernel

The Hund Kernel is the runtime's logical core. It owns lifecycle transitions, policy evaluation, resource accounting, event routing and service registration.

Initial implementation must remain host-independent and depend only on contracts. It is not a replacement for the Android, Windows or Linux kernel.
