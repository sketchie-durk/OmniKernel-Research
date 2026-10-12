# OmniKernel: Architectural Specification v1.0

OmniKernel is a synthetic hybrid-kernel architecture designed for the study of systemic vulnerability patterns. It combines the performance of a monolithic kernel with the isolation properties of a microkernel.

## 1. Memory Management
OmniKernel utilizes a **Capability-Based Addressing** model. Every memory access requires a capability token that defines the permissible operations (Read, Write, Execute) and the memory bounds.

### 1.1 The Virtual Page Table (VPT)
The VPT is managed by a privileged Memory Management Unit (MMU) handler. Page table entries (PTEs) are signed with a kernel-level HMAC to prevent unauthorized modification by compromised drivers.

## 2. The OmniCall Interface
System calls are routed through a unified gateway called the **OmniCall Interface**. 

### 2.1 Syscall Dispatch
OmniCall uses a register-based dispatch mechanism. The `OmniCallID` determines the target subsystem. The interface performs strict validation of all input pointers against the calling process's capability set before dispatching to the handler.

## 3. Inter-Process Communication (IPC)
IPC is implemented via **Tunnels**. A Tunnel is a bidirectional, kernel-managed queue between two processes.

### 3.1 Tunnel Synchronization
Tunnels use a non-blocking, asynchronous notification system. When a message is placed in a Tunnel, the receiving process is notified via a kernel-level event signal.

## 4. The FastPath Extension
To reduce transition overhead, OmniKernel implements **FastPath**. FastPath allows specific user-mode buffers to be mapped directly into kernel space for high-throughput operations, bypassing the standard OmniCall validation for predefined memory regions.
