# Adaptive Routing for Hybrid Photonic–Electronic Computing

## High-level concept note

**Draft for general publication · October 2026**

### Abstract

Photonic processors and optical interconnects can move and transform selected data at high bandwidth, while electronic processors remain well suited to control flow, memory access, and precise stateful operations. A heterogeneous system therefore needs to decide where each operation should run, taking account of the full path from input through computation to verified output. This concept proposes a general runtime coordination layer that observes workload needs and device conditions, estimates end-to-end cost, and routes work among electronic, photonic, hybrid, or direct-transfer paths. The layer would account for conversion, setup, queueing, precision, validation, and recovery costs. The proposal is a research direction, not a claim that photonic computing already outperforms CPUs or GPUs. A Linux-runnable scenario model has been used to explore the control policy, but its assumed device costs and link conditions are not hardware measurements. The key research question is whether adaptive end-to-end routing can improve useful throughput, energy per correct result, or resilience for suitable workloads.

### 1. Motivation

Optical systems can support high-bandwidth interconnects and parallel linear operations. Research has demonstrated integrated photonic processors for neural-network operations, while separate work has demonstrated programmable optical interconnects and switching. These results point toward systems that combine photonic and electronic resources rather than requiring every operation to use one processing medium [1–3].

The performance of a photonic operation depends on more than the speed of the optical device. Data may need conversion between electrical and optical forms; a task may require precision or memory behavior that a photonic unit does not provide; and a busy, degraded, or unreliable path can erase the expected benefit. A scheduler that considers only nominal compute speed can therefore select a path that performs poorly end to end.

### 2. Proposed concept

The proposed system adds a runtime coordination layer between applications and heterogeneous compute resources. For each eligible task, it would consider:

- the operation type, precision requirement, data size, and deadline;
- current queueing and availability across compute resources;
- optical-link or photonic-device quality;
- input/output conversion, setup, validation, and possible retry costs; and
- the expected cost of using an electronic, photonic, hybrid, or direct-transfer path.

The coordinator would select a path only when its expected end-to-end result meets the task’s correctness and service requirements. It would monitor the result and resource conditions, then redirect later work when conditions change. If no accelerated path offers a measured benefit, the task can remain on its ordinary execution path.

This proposal concerns orchestration across resources. It does not require a new optical encoding format, a new processor instruction set, or replacement of general-purpose CPUs and GPUs.

### 3. Testable hypotheses

1. For workloads dominated by suitable parallel operations, adaptive routing can improve useful throughput or energy per correct result compared with electronic-only execution and fixed photonic offload.
2. Including conversion, queueing, precision, validation, and retry costs in the routing decision can reduce wasted offloads during degraded conditions.
3. Batching compatible work can amortize setup and framing costs when the throughput gain exceeds the added buffering latency and recovery cost.
4. A hybrid system can preserve general-purpose electronic execution for control, memory, and precision-sensitive tasks while using photonic resources selectively.

These are hypotheses for measurement. They are not results established by the current scenario model.

### 4. Evaluation plan

Compare at least three configurations using the same workloads and correctness targets:

1. electronic execution only;
2. fixed photonic offload for tasks designated as suitable; and
3. adaptive routing that accounts for runtime conditions and end-to-end cost.

Workloads should include dense linear operations, control-heavy tasks, precision-sensitive operations, memory-bound tasks, and mixed production-style traces. Tests should include both steady conditions and stress periods with changing device quality, queue pressure, resource failures, and recovery.

Report useful throughput, median and tail latency, energy per correct result, numerical error, retry and fallback rates, and routing overhead. Any photonic and electronic baselines should use equivalent output quality and include conversion and host-processing costs. Micro-batching should be evaluated at several batch sizes with latency and retry costs reported alongside throughput.

### 5. Current status and limitations

A software scenario model has been run on Linux to exercise path-selection policies under synthetic workload and optical-quality changes. Its device service times, energy values, and quality profile are assumed inputs. The model is useful for exploring policy behavior and designing later experiments; it does not measure optical hardware or establish performance relative to a real CPU or GPU.

The main technical risks include photonic precision and noise, conversion overhead, memory and control-flow requirements, device variability, workload misclassification, and routing decisions that oscillate as conditions change. Hardware measurements and repeatable workload traces are required before making claims about practical benefit.

### 6. Scope of the publication concept

This note presents a general research direction: runtime coordination for hybrid photonic–electronic computing. It does not claim that optical computation is new, that adaptive optical switching is new, or that the proposed approach has demonstrated a hardware advantage. The potential contribution to investigate is the end-to-end policy that selects among compute and transfer paths using task requirements, live resource conditions, and measured expected benefit.

### References

1. Z. Xie, D. Sánchez-Jácome, L. Torrijos-Morán, and D. Pérez-López, “Software-defined optical networking applications enabled by programmable integrated photonics,” *Journal of Optical Communications and Networking*, vol. 16, pp. D10–D17, 2024. https://doi.org/10.1364/JOCN.521505
2. “Single-chip photonic deep neural network with forward-only training,” *Nature Photonics*, vol. 18, pp. 1335–1343, 2024. https://www.nature.com/articles/s41566-024-01567-z
3. “Low-power scalable multilayer optoelectronic neural networks enabled with incoherent light,” *Nature Communications*, vol. 15, article 10692, 2024. https://doi.org/10.1038/s41467-024-55139-4
