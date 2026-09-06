---
type: project
status: active
date: 2026-08-24
tags:
  - metallothioneins
  - oryza-coarctata
  - manuscript
---

# OcMT Manuscript — MOC

The only file you open first. Everything else links out from here.

> [!info] What this project is
> The writing/synthesis layer for the *O. coarctata* metallothionein work. It does not hold raw data or protocols itself — those live in the four source projects below. This is where the pieces get pulled into one manuscript.

## This project's own files

- [[Writing]] — drafts, abstract thinking, figure/table planning
- [[Discussion]] — supervisor meetings, feedback, deadlines
- [[Log]] — chronological progress notes for the manuscript itself

## Source projects feeding this manuscript

| Project | Contributes | MOC |
|---|---|---|
| Homolog identification | Gene family ID, phylogeny, promoter analysis | [[01_OC_homolog MOC]] |
| *O. sativa* knockout | Functional validation, transgenic lines | [[02_OS_Knockout MOC]] |
| Molecular dynamics | Structural/Zn-binding simulation | [[03_Molecular_Dynamics_of_OC MOC]] |
| Single-cell | Cell-type-resolved expression (ortholog projection) | [[04_SC_of_metallothionein MOC]] |

## Everything tagged for this manuscript

```dataview
TABLE type AS Type, status AS Status, file.folder AS Folder, file.mtime AS Touched
FROM ""
WHERE contains(string(project), "OcMT-manuscript")
SORT file.mtime DESC
```

## Papers relevant to this manuscript

```dataview
TABLE citekey AS Key, year AS Year, status AS Status
FROM "03_Resources/Literature"
WHERE type = "paper"
SORT year DESC
```

## Open threads

- [ ] Draft the outline once phylogenetic placement (01_OC_homolog) and single-cell projection (04_SC_of_metallothionein) results are in
- [ ] Decide target journal
