---
type: moc
project: 02_knocout_os
moc_id: 01309298993
status: active
tags:
  - meta
  - oryza-sativa
  - crispr
  - knockout
  - transgenic
---

# 02 Knockout OS — Map of Content

01309298993

> [!info] Scope
> Confirmation and functional work on transgenic / CRISPR *OCMT* (*Oryza coarctata*
> metallothionein) lines in *Oryza sativa* cv. **BRRI Dhan67 (BR67)** — verifying the
> transgene is present in each T3 line before any downstream phenotyping, plus the
> genome-editing design choices.

## Experimental design

![[02_knockout_os_experimental_design.excalidraw]]

## Experiment line-up

1. Check whether *OCMT* is present in the transgenic lines
	1. [[BR-67 T3 DNA Extraction (2026-09-03)]]
	2. [[02_knocout_os_e001_pcr_mt_confirmation_t3]] — PCR (with primer), 25 T3 BR67 plants
2. In planta / CRISPR
	1. [[Alam et al 2022]] — reference paper (OsbHLH024 knockout via CRISPR/Cas9, salt stress in rice); design notes point at a not-yet-created [[proposal os knockout]] plan
	2. [[CRISPR Cas9 Knockout]] — mechanism primer (gRNA → Cas9 cut → indel repair → knockout)

## Protocols

- [[02_knocout_os_ctab_dna_extraction_protocol]] — CTAB genomic DNA extraction from rice young leaf (bench wording)
- [[DNA_extraction_short_method_real_world_guide]] — detailed real-world walkthrough of the short (SDS-based) extraction method, step-by-step with troubleshooting per step

### Reagent notes (CTAB protocol background)

- [[CTAB]] — why CTAB, buffer composition table, 60 °C rationale
- [[β-mercaptoethanol]] — disulfide reduction + anti-browning role, safety warning
- [[Sodium acetate]] — precipitation chemistry, concentration/volume/pH rationale

## Experiments

- [[02_knocout_os_e001_pcr_mt_confirmation_t3]] — OS-E001: PCR confirmation of the MT transgene in T3 plants (stage 1, iter 1)

## Line registries

- [[OCMT Transgenic Line Registry (BRRI Dhan67)]] — in planta *OCMT* over-expression lines, `p-<line>-<sub>` IDs

## Design references

- [[02_knocout_os_osu3_vs_osu6_promoter]] — why `OsU6` beats `OsU3` for sgRNA expression in rice editing

## Everything in this project (auto)

```dataview
TABLE type AS Type, status AS Status, file.mtime AS Touched
FROM "02_knocout_os"
WHERE file.name != this.file.name
SORT file.mtime DESC
```

## Open tasks (auto)

```dataview
TASK
FROM "02_knocout_os"
WHERE !completed
```
