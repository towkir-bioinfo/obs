---
type: home
tags:
  - meta
---

# Home

## Open tasks (auto)

```dataview
TASK
FROM -"Clippings" AND -"Excalidraw"
WHERE !completed
GROUP BY file.link
```

## Due / dated tasks (auto)

```dataview
TASK
FROM -"Clippings" AND -"Excalidraw"
WHERE !completed AND due
SORT due ASC
```

## Active projects

- [[01_homolog_oc/01_homolog_oc_moc]] — Homolog OC
- [[02_knocout_os/02_knocout_os_moc]] — Knockout OS
- [[03_adenocarcenoma_single_cell/03_adenocarcenoma_single_cell_moc]] — Adenocarcinoma Single-Cell
- [[04_cblast/04_cblast_moc]] — cBLAST

## Recently touched (auto)

```dataview
TABLE type AS Type, status AS Status, file.mtime AS Touched
FROM -"Clippings" AND -"Excalidraw" AND -"Home"
SORT file.mtime DESC
LIMIT 10
```

## Quick links

[[Paper.base]]

[[Course.base]]
