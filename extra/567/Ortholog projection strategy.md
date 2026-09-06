---
type: note
project: "[[04_SC_of_metallothionein MOC]]"
status: active
date: 2026-08-20
tags:
  - single-cell
  - strategy
  - scope
  - metallothioneins
---

# Ortholog projection strategy

The scope decision for the single-cell arm of the MT work. Settles what is and is not buildable.

## The core problem

Study a rice gene family (metallothioneins) in the wild halophyte *Oryza coarctata*, using single-cell data — data that says which specific cell type makes each gene.

## The three constraining facts

1. **No single-cell data exists for *O. coarctata*.** It cannot be downloaded. Building it requires a single-cell sequencer and real plant tissue.
2. **Single-cell data does exist for *O. sativa*,** produced by other labs, and is downloadable — see [[Oryza sativa scRNA-seq datasets]].
3. **A new atlas cannot be built for either species right now:**
   - *coarctata* — no single-cell data exists to build one from
   - *sativa* — several complete atlases already exist; another is duplication, not new work

## What is actually doable

> [!important] One sentence
> Look up the MT genes in other people's rice atlases, then infer where the matching genes sit in *coarctata*.

1. Take an existing single-cell rice map; locate the metallothionein genes inside it.
2. Read off what it says — e.g. "active in root epidermal cells", or "induced under salt stress in this one cell type".
3. Find the matching *coarctata* gene (the ortholog).
4. Write: *"Based on rice, we predict this coarctata gene behaves the same way."* **This is a prediction, not a measurement** — state it as such.
5. Later, test the prediction at the bench with a cheap targeted method — no sequencer needed, just a small root tissue piece and a basic assay.

No atlas-building. No new sequencing. Borrow existing data, locate the genes, make a disciplined inference.

## Next steps

- [ ] Pull exact accession numbers for the three unresolved entries (Zhao 2023; single-cell multi-omics atlas 2025; Wang 2021) via direct DOI fetch
- [ ] Search Expression Atlas / SRA systematically for additional *O. sativa* salt-stress bulk RNA-seq beyond the current table
- [ ] Build the download script for confirmed accessions
- [ ] Run the protoplasting-artifact check on MT genes using the Zhu 2025 induced-gene list before trusting any MT signal

## Related

- [[Single-cell atlas]]
- [[Oryza coarctata data inventory]]
- [[Plant single-cell atlas databases]]
- [[2026-08-20]]
