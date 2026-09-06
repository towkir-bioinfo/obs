---
type: note
date: 2026-08-18
tags:
  - single-cell
legacy-status: reference
---
>[!info] Defination:
> In single-cell transcriptomics, "delineating" refers to resolving discrete cell populations or states by their transcriptional differences rather than by morphology alone. It underlies clustering, cell-type annotation, and developmental trajectory reconstruction — the quality of delineation depends on marker gene availability and clustering resolution.




```dataview
TABLE file.cday AS "Created Date"
FROM [[#]] AND -"_templates"
WHERE status = "active" OR "reference"
SORT file.cday DESC
```

