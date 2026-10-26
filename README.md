# Adaptive Routing for Hybrid Photonic–Electronic Computing

## Concept overview

This project explores a research concept for coordinating electronic processors, photonic processors, and optical interconnects at runtime. A coordination layer would estimate the end-to-end cost of eligible work—including data conversion, queueing, setup, precision, validation, and recovery—and choose a path that meets the task’s correctness and service requirements.

The aim is to test whether this kind of adaptive routing can improve useful throughput, energy per correct result, or resilience for suitable workloads. It is a systems-orchestration concept; it does not propose a new optical encoding format or claim that photonic computing already outperforms CPUs or GPUs.

## Read the concept note

[Adaptive Routing for Hybrid Photonic–Electronic Computing](adaptive_photonic_electronic_concept_note.md)

## Current status

A Linux-runnable software scenario model has been used to explore routing policies under synthetic workload and device-quality assumptions. It is not a hardware benchmark and does not establish a performance advantage. The concept note describes limitations and a plan for controlled future evaluation.

## Suggested evaluation

Compare electronic-only execution, fixed photonic offload, and adaptive routing on the same workloads and correctness targets. Include conversion and host-processing costs; report useful throughput, latency, energy per correct result, numerical error, retry rates, and routing overhead.

## Scope

This repository contains a high-level public concept note. Its claims are framed as research hypotheses, not demonstrated results.
