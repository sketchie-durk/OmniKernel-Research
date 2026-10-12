# OmniKernel: Hardware Abstraction Layer (HAL)

The OmniKernel HAL defines the interaction between the kernel and the synthetic hardware.

## 1. Synthetic CPU: The OmniCore
The OmniCore is a RISC-based processor with a specialized **Tainted-Bit** architecture. Every register has a hidden bit that tracks whether the data originated from an untrusted (User-Mode) source.

## 2. Cache Architecture
The OmniCore uses a 3-level cache hierarchy.
- **L1/L2**: Private per core.
- **L3**: Shared across cores.

## 3. Side-Channel Surface: The Speculation Buffer
The OmniCore implements aggressive branch prediction. The **Speculation Buffer** stores transient results of predicted paths. If a prediction is wrong, the results are discarded, but the state of the L1 cache remains modified.
