---
type: moc
project: 01_homolog_oc
moc_id: 01309298993
status: active
tags:
  - meta
  - oryza-coarctata
  - homology
---

# 01 Homolog OC — Map of Content

01309298993

> [!info] Scope
> Genome-wide identification of metallothionein homologs in the *Oryza coarctata*
> proteome: Pfam **PF01439** (Metallothio_2) → `hmmsearch` → E-value / score filter →
> candidate extraction → `blastp` verification against the Bansal/Pcoar assembly →
> ProtParam characterisation → MAFFT alignment, then expression profiling under
> salt / submergence stress.

## Start here

- [[01_homolog_oc_homolog_finder_protocol]] — the protocol of record; bench/dry-lab steps, analysis directory, proteome + profile paths
- [[01_homolog_oc_homolog_reanalysis_pipeline]] — current end-to-end pipeline (domain search → cross-assembly mapping → expression), with the candidate-count flow diagram

## Pipeline & protocols

- [[01_homolog_oc_homolog_pipeline_draft]] — earlier written-out workflow (Pfam download, hmmsearch vs hmmscan, tool choices)
- [[01_homolog_oc_genome_wide_homology_notes]] — tools / papers / method scratch notes
- [[01_homolog_oc_homolog_finder_protocol_original_backup]] — original unedited copy of the finder protocol (archived)

## Scripts

- [[01_homolog_oc_homolog_finder_bash_script]] — *stub*
- [[01_homolog_oc_homolog_finder_in_oc_proteome]] — *stub*

## Logs

- [[01_homolog_oc_log_2026-08-04]] — data download + Pfam profile retrieval

## Provenance

- [[01_homolog_oc_protocol_lineage]] — which analysis ran first, and what superseded it

## Everything in this project (auto)

```dataview
TABLE type AS Type, status AS Status, file.mtime AS Touched
FROM "01_homolog_oc"
WHERE file.name != this.file.name
SORT file.mtime DESC
```

## Open tasks (auto)

```dataview
TASK
FROM "01_homolog_oc"
WHERE !completed
```
