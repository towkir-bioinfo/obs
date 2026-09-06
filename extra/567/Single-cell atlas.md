---
type: note
date: 2026-08-20
tags:
  - single-cell
  - atlas
legacy-status: reference
---
>[!info] Defination:
> The systematic process of creating a comprehensive, high-resolution reference map of every cell type, state, and location within a tissue, organ, or entire organism.

Source: [Building Comprehensive Single-Cell Atlases — Biocompare](https://www.biocompare.com/Editorial-Articles/620913-Building-Comprehensive-Single-Cell-Atlases/)

## Why it matters here

An atlas is a *reference*, not a single experiment. Building one requires single-cell sequencing capacity plus real tissue. Where no atlas exists for a species, the practical route is projection from a related species' atlas — see [[Ortholog projection strategy]].

## Status in plants

| Progress status | Species | What is available |
|---|---|---|
| Fully mapped (entire life cycle) | *Arabidopsis thaliana* | >400,000 cells, seed to mature plant |
| Highly detailed (specific tissues) | Rice, maize, wheat, tomato, tobacco | Deep single-cell data for root systems, leaves, shoots |
| Emerging / unmapped | Rare wild plants, complex trees, medicinal herbs | Often blocked by tough cell walls or unsequenced genomes |

## Related

- [[Plant single-cell atlas databases]]
- [[Bulk RNA-seq]]
- [[Usman et al 2025]]

```dataview
TABLE file.cday AS "Created Date"
FROM [[#]] AND -"_templates"
WHERE status = "active" OR "reference"
SORT file.cday DESC
```
