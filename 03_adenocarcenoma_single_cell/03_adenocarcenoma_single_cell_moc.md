---
type: moc
project: 03_adenocarcenoma_single_cell
moc_id: 01309298993
status: active
tags:
  - meta
  - single-cell
  - cancer
  - scRNA-seq
---

# 03 Adenocarcinoma Single-Cell — Map of Content

01309298993

> [!info] Scope
> Single-cell transcriptomic analysis of tumour tissue (pediatric solid tumours /
> neuroblastoma, patient material from UZ Ghent). Covers dataset integration across
> studies (scVI), batch-effect handling, and downstream biomarker / drug-target
> readouts. This is the **cancer** single-cell arm — separate from the plant
> metallothionein single-cell work still sitting in `extra/567/`.

## Start here

- [[03_adenocarcenoma_single_cell_star_methods_template]] — STAR★Methods sheet: key resources table, samples, reagents, ethics (UZ Ghent EC 2019/1428)

## Analysis & diagrams

- [[03_adenocarcenoma_single_cell_integration_diagram.excalidraw]] — study-by-study cell counts, scVI integration, batch effects, biomarker → drug-target flow

## Disease notes

- [[03_adenocarcenoma_single_cell_neuroblastoma_notes]] — *stub*

## Everything in this project (auto)

```dataview
TABLE type AS Type, status AS Status, file.mtime AS Touched
FROM "03_adenocarcenoma_single_cell"
WHERE file.name != this.file.name
SORT file.mtime DESC
```

## Open tasks (auto)

```dataview
TASK
FROM "03_adenocarcenoma_single_cell"
WHERE !completed
```
