---
type: note
project: "[[04_SC_of_metallothionein MOC]]"
status: active
date: 2026-08-20
tags:
  - oryza-sativa
  - single-cell
  - datasets
  - accessions
---

# *Oryza sativa* — single-cell & reference datasets

**Representative, not exhaustive.** Bulk RNA-seq studies on rice number in the thousands; an exhaustive table is not a table anyone reads. Selected: single-cell atlases, salt-stress bulk datasets, and major reference resources — the set relevant to the MT/salt-stress work.

| Study (APA) | Details | DOI | Data repo | Comment |
|---|---|---|---|---|
| Zhang, T.-Q., Chen, Y., Liu, Y., Lin, W.-H., & Wang, J.-W. (2021). Single-cell transcriptome atlas and chromatin accessibility landscape reveal differentiation trajectories in the rice root. *Nature Communications*, 12, 2053. | scRNA-seq + scATAC-seq, radicle root tip, 28,857 cells | 10.1038/s41467-021-22352-4 | [E-ENAD-52](https://ebi.ac.uk/gxa/sc/experiments/E-ENAD-52) | Best single-cell reference for root marker sets. Control tissue only — no stress condition. |
| Wang, Y., Huan, Q., Li, K., & Qian, W. (2021). Single-cell transcriptome atlas of the leaf and root of rice seedlings. *Journal of Genetic Genomics*, 48, 881–898. | scRNA-seq, leaf + root, control and multiple abiotic stresses (incl. salt), 237,431 cells | 10.1016/j.jgg.2021.06.001 | GEO — accession stated in paper, confirm on publisher page | **Only rice scRNA-seq atlas with an explicit stress-condition design. Primary marker-projection source.** |
| A single-cell multi-omics atlas of rice. (2025). *Nature*. | scRNA-seq + scATAC-seq, 116,564 cells, 8 organs, joint GRN inference | 10.1038/s41586-025-09251-0 | Per data-availability statement — not resolved here | Cell-type-resolved ACRs — the resource for the promoter-motif cross-reference step. |
| Zhu, M., Hsu, C.-W., Peralta Ogorek, L.-L., et al. (2025). Single-cell transcriptomics reveal how root tissues adapt to soil stress. *Nature*, 642, 721–729. | scRNA-seq + spatial, root; gel vs. soil vs. compacted soil; >79,000 cells | 10.1038/s41586-025-08941-z | [PRJNA1055099](https://ncbi.nlm.nih.gov/bioproject/PRJNA1055099) (GSE251706); prior PRJNA706435 / PRJNA706099 | Includes explicit protoplasting-induced gene list (GSE283509/GSE260671) — **mandatory for the MT-artifact check.** |
| Feng, D., Liang, Z., Wang, Y., et al. (2022). Chromatin accessibility illuminates single-cell regulatory dynamics of rice root tips. *BMC Biology*, 20, 274. | scATAC-seq, root tips, normal vs. heat stress, 46,758 cells | 10.1186/s12915-022-01473-2 | NCBI (accession in paper) | Chromatin only, no matched transcriptome. Useful for ACR cross-referencing under a different stress than salt. |
| Zong, J., Wang, L., Zhu, L., et al. (2022). A rice single cell transcriptomic atlas defines the developmental trajectories of rice floret and inflorescence meristems. *New Phytologist*. | scRNA-seq, inflorescence/floret, 37,571 cells | 10.1111/nph.18008 | Accession in paper | Not stress-related; include only if MT expression work extends to reproductive tissue. |
| Liu, Q., Liang, Z., Feng, D., et al. (2021). Transcriptional landscape of rice roots at the single-cell resolution. *Molecular Plant*, 14, 384–394. | scRNA-seq, root, control | 10.1016/j.molp.2020.11.017 | Accession in paper | Earliest rice root scRNA-seq; largely superseded. Keep for backward citation only. |
| RiceXPro (database, not a study) | Curated microarray/RNA-seq across organs and stages, japonica cv. Nipponbare | — | [ricexpro.dna.affrc.go.jp](https://ricexpro.dna.affrc.go.jp) | Processed expression browser, not raw data. Fast bulk-level MT sanity check. |
| Expression Atlas – *Oryza sativa* (EBI) | Aggregated bulk + single-cell experiments across studies | — | [ebi.ac.uk/gxa](https://www.ebi.ac.uk/gxa/experiments?species=oryza%20sativa) | Search hub, not one dataset. Use to locate additional salt-stress bulk studies. |

## Related

- [[Oryza coarctata data inventory]]
- [[Ortholog projection strategy]]
- [[Liu et al., 2021]] · [[Wang et al., 2021]]
- [[2026-08-20]]
