# Resource Monitoring & Performance Analysis

## Objective

The objective of this phase was to monitor and analyze the
Linux system's CPU, memory, swap, disk, and overall resource
utilization.

Resource monitoring helps administrators identify performance
issues, resource exhaustion, unusual workloads, and potential
system bottlenecks.

---

## 1. CPU Analysis

The CPU architecture and available processing resources were
identified using:

```bash
lscpu | grep -E '^(CPU\(s\)|Model name|Thread|Core|Socket)'

#Observed Configuration

| Resource         | Value                        |
| ---------------- | ---------------------------- |
| Logical CPUs     | 8                            |
| CPU Cores        | 4                            |
| Threads per Core | 2                            |
| CPU Socket       | 1                            |
| CPU Model        | Intel Core i7-4770 @ 3.40GHz |
