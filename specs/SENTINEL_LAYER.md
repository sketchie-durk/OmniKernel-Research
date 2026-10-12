# OmniKernel: The Sentinel Layer Specification v1.0

The Sentinel Layer is a kernel-integrated observability engine designed to detect and neutralize Entropic State Decay in real-time.

## 1. Invariant Monitoring
The Sentinel Layer maintains a set of **Systemic Invariants**. An invariant is a condition that must *always* be true for the kernel to be in a secure state.
*Example*: `Invariant-01: A FastPath buffer must never be modified by User-Mode during a Kernel-Mode read operation.`

## 2. Primitive Detection Hooks
The Sentinel Layer implements "Shadow-Hooks" at every major state transition (OmniCall, Tunnel dispatch, Context switch). These hooks evaluate the current state against the Invariant set.

## 3. Reactive Neutralization
Upon detecting an Invariant violation, the Sentinel Layer does not simply crash the system (Panic). Instead, it performs a **State-Rollback**:
1. Freezes the offending process.
2. Reverts the kernel state to the last known-good checkpoint.
3. Terminates the process and logs the "Primitive Pattern" for synthesis in the Grimoire.
