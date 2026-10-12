# OmniKernel: Scheduler Specification v1.0

The OmniKernel Scheduler manages process execution using a **Dynamic Priority-Weighted Round Robin (DPWRR)** algorithm.

## 1. Priority Classes
OmniKernel defines four priority classes:
- `CLASS_REALTIME`: Guaranteed CPU slice, non-preemptible.
- `CLASS_SYSTEM`: High priority, used for kernel-critical drivers.
- `CLASS_INTERACTIVE`: Dynamic priority based on I/O wait times.
- `CLASS_BATCH`: Lowest priority, used for background computation.

## 2. The Ready Queue
The scheduler maintains a set of per-CPU ready queues. Each queue is a red-black tree sorted by the `Effective Priority` of the process.

## 3. Context Switching
Context switches are triggered by the `OmniTimer` interrupt or explicit `yield` calls. The kernel saves the process state (registers, capability tokens, and stack pointer) into the Process Control Block (PCB).

## 4. Priority Boosting
To prevent starvation, OmniKernel implements **Priority Boosting**. Processes in `CLASS_BATCH` that have not received CPU time for `N` cycles are temporarily boosted to `CLASS_INTERACTIVE`.
