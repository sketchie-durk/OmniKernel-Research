# Research Guidelines: Systemic Analysis

The objective of the OmniKernel project is to move from "bug hunting" to "systemic analysis." Researchers are encouraged to follow this methodology:

## 1. Primitive Identification
Instead of seeking a single crash, identify a **Primitive**. 
*Example*: "The ability to trigger a state-desync in the Tunnel handler."

## 2. Chain Construction
Once a primitive is identified, construct a chain to achieve a target goal (e.g., Privilege Escalation).
*Chain Example*: `[Heap Grooming] -> [Tunnel UAF] -> [Capability Token Overwrite] -> [Kernel Execution]`.

## 3. Mitigation Design
For every discovered vulnerability, a corresponding architectural mitigation must be proposed.
*Example*: Implementing a double-buffered validation check for FastPath to eliminate TOCTOU.
