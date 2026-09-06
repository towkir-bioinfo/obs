---
type: note
date: 2026-08-18
tags:
  - transcriptomics
legacy-status: reference
---
>[!info] Defination:
> Sequencing of pooled RNA extracted from a whole tissue or cell population, yielding one averaged expression profile per sample rather than per cell. This averaging masks cell-to-cell transcriptional heterogeneity, rare cell populations, and cell-type-specific regulatory networks — the limitation that motivates single-cell approaches (scRNA-seq).




```dataview
TABLE file.cday AS "Created Date"
FROM [[#]] AND -"_templates"
WHERE status = "active" OR "reference"
SORT file.cday DESC
```

