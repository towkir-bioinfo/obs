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

- [[01_homolog_oc_homolog_reanalysis_pipeline]] *(analysis · 2026-08-24 · active)* — the current pipeline; 3 stages (domain search → cross-assembly `blastp` mapping → salt/submergence expression), Mermaid flow diagram and runnable bash. GWH proteome 68,177 seqs → 15 MT-domain candidates → 7 Bansal `Pcoar_v1.1` gene IDs. Alias: *MT Pipeline Guide*.
- [[01_homolog_oc_homolog_finder_protocol]] *(protocol · 2026-08-11 · active)* — the protocol of record the reanalysis followed; 11 sections (Pfam/HMMER → filtering → bias % → candidate extraction → BLAST → ProtParam → MAFFT). Records the analysis directory and proteome/profile paths. Result / Interpretation / Next-iteration still unwritten; candidate count differs between sections (11 IDs in §7 vs 8 in §9) — confirm which set is current before citing.

## Pipeline & protocols

- [[01_homolog_oc_homolog_pipeline_draft]] *(protocol · 2026-08-16 · reference)* — earlier written-out workflow: Pfam download path, `hmmsearch` vs `hmmscan` decision table, full absolute-path HMMER commands incl. `--domtblout`. Superseded by the reanalysis pipeline.
- [[01_homolog_oc_genome_wide_homology_notes]] *(scratch · near-empty)* — bare tools/papers/method skeleton (only entry: [[HMMER]]); legacy frontmatter not cleaned.
- [[01_homolog_oc_homolog_finder_protocol_original_backup]] *(archive · ~1.8 MB)* — original unedited copy of the finder protocol, kept for provenance.

## Scripts

- [[01_homolog_oc_homolog_finder_bash_script]] — *stub, placeholder only*
- [[01_homolog_oc_homolog_finder_in_oc_proteome]] — *stub, placeholder only*

## Logs

- [[01_homolog_oc_log_2026-08-04]] *(log · 2026-08-04)* — day 1: downloaded the NGDC GWH assembly (37798) and retrieved the [[PF01439]] Pfam profile; embeds the legacy bioinformatics protocol. Tasks done: data download ✅, Pfam ✅.

## Provenance

- [[01_homolog_oc_protocol_lineage]] *(note · active)* — one-line lineage: finder protocol ran first, reanalysis pipeline is the re-run.

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
