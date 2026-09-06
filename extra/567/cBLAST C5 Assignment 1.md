---
type: note
project: "[[cBLAST]]"
date: 2026-08-16
tags:
  - proteomics
  - mass-spectrometry
  - meta
---

# cBLAST C5 Assignment 1

Proteomics assignment: SILAC-based quantification with MaxQuant, using two
sample raw files and a human proteome background database.

> [!info] Submission
> Single PDF file. [Assignment link](https://cblast.du.ac.bd/mod/assign/view.php?id=535)

## Question

Download the attached files where you will get two sample raw files and one
file for human proteome as background database. The sample raw data were
obtained using SILAC Quantification method. Use provided data for MaxQuant
analysis and find the answers for following questions.

## Tasks

- [ ] How many peptides were found in total in sample1 and sample2? — **3 marks**
- [ ] How many proteins identified and quantified after removing converted and reverted protein? — **3 marks**
- [ ] Which protein(s) show highest intensity? — **2 marks**
- [ ] Which protein shows highest score? — **2 marks**
- [ ] Heatmap of sample1 and sample2 — **5 marks**
- [ ] Heatmap (adding isotope pattern), chromatogram, and 3D viewer for the highest-intensity protein(s) — **5 marks**
- [ ] Generate all possible maps for the 47th peptide, `AAPLDSIHSLAAYYIDCIR` — **10 marks**

**Total: 30 marks**

## Notes

- 47th peptide of interest: `AAPLDSIHSLAAYYIDCIR`

> [!warning] Wording preserved as given
> "removing converted and reverted protein" is kept verbatim from the source
> text. In MaxQuant output this task most likely means filtering out
> **Potential contaminant** and **Reverse** hits from `proteinGroups.txt` — but
> that's a guess, not a correction, so the original wording stands.
