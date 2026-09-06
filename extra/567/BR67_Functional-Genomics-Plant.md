---
type: project
status: inactive
date: 2026-08-16
tags:
  - gene-family
  - functional-genomics
---

# BR67 Functional Genomics — Plant

Functional characterization of the metallothionein family in the BR67 rice cultivar. BR67 is a salt-tolerant variety; this project investigates the genetic basis of tolerance through a candidate-gene approach targeting metallothionein genes and their regulatory elements.

## Question

What is the genetic basis for the enhanced salinity tolerance observed in BR67 rice? Specifically, how do metallothionein genes and their promoter architecture contribute to this phenotype?

## Why it matters

Salt stress is a major abiotic constraint in rice cultivation globally. Understanding the genetic mechanisms underlying tolerance in BR67 can inform breeding strategies for salt-tolerant varieties. Metallothioneins are known to participate in both ROS scavenging and metal ion homeostasis under stress.

## Scope — in

Plant line development and characterization (wet-lab genetics). Transgenic line generation and T3 seed production. Phenotyping under salt stress. Expression analysis of candidate MT genes under control and stress conditions.

## Scope — out

Protein-level validation, metal-binding assays, mechanistic biochemistry. Those become a separate project if the expression data justify them.

## Plant Lines

**Master registries:**

1. **[[02_knocout_os_br67_mt_plant_lines_registry]]** — T3 generation lines (16 MT transgenic + 7 WT controls)
2. **[[BR67_PVA-ASR_Transgenic-Lines]]** — Multi-population T1/T4 registry with ASR1 and PVA1 promoter constructs

### Summary

| Population | Construct | Background | Count | Notes |
|---|---|---|---|---|
| MT lines | Metallothionein OE | BR75 + BR81 | 16 T4 + 7 WT | Your working population |
| ASR1 lines | ASR1 promoter-driven | BR75 | 30+ | T1 seeds in PBT |
| PVA1 (BR81) | PVA1 promoter-driven | BR81 | 6 | T1 seeds in PBT |
| PVA1 (BR75) | PVA1 promoter-driven | BR75 | 90+ | T1 seeds in PBT |

## Experiments

```dataview
TABLE stage AS Stage, iteration AS Iter, status AS Status, file.mtime AS Touched
FROM ""
WHERE type = "experiment" AND contains(string(project), "BR67_Functional-Genomics-Plant")
SORT stage ASC
```

## Papers

```dataview
TABLE citekey AS Key, year AS Year, status AS Status
FROM ""
WHERE type = "paper" AND contains(string(project), "BR67_Functional-Genomics-Plant")
SORT year DESC
```

## Log
