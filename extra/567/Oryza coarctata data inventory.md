---
type: note
project: "[[04_SC_of_metallothionein MOC]]"
status: active
date: 2026-08-20
tags:
  - oryza-coarctata
  - datasets
  - accessions
  - salt-stress
---

# *Oryza coarctata* — data inventory

Near-complete. Total published RNA-seq datasets for this species number under ten, all findable.

> [!warning] Accession discipline
> "Not resolved here" means the search snippet did not surface the exact accession string. The DOI page's Data Availability section will have it — **do not guess or fabricate an accession number.**

## Transcriptomic studies

| Study (APA)                                                                                                                                                                                          | Details                                                                                           | DOI                          | Data repo                                                                                                                   | Comment                                                                                                                                       |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- | ---------------------------- | --------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Mondal, T. K., Ganie, S. A., & Debnath, A. B. (2015). Identification of novel and conserved miRNAs from extreme halophyte, *Oryza coarctata*, a wild relative of rice. *PLOS ONE*, 10(10), e0140675. | Small RNA-seq, 2 libraries (control vs. 450 mM NaCl, 24 h), leaf                                  | 10.1371/journal.pone.0140675 | [PRJNA271658](https://ncbi.nlm.nih.gov/bioproject/PRJNA271658) (SRX831195)                                                  | Small RNA only, not mRNA. Useful for miRNA-target prediction on MT paralogs.                                                                  |
| Garg, R., Verma, M., Agrawal, S., Shankar, R., Majee, M., & Jain, M. (2014). Deep transcriptome sequencing of wild halophyte rice, *Porteresia coarctata*… *DNA Research*, 21(1), 69–84.             | mRNA-seq; control/salt450/salt700/submergence/salt+submergence; ~375M reads; de novo assembly     | 10.1093/dnares/dst042        | [GSE44913](https://ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE44913)                                                         | First large-scale coarctata transcriptome. De novo assembled — expect fragmented/redundant transcripts, remap to Zhao 2023 genome before use. |
| Bansal, J., Gupta, K., Rajkumar, M. S., Garg, R., & Jain, M. (2021). Draft genome and transcriptome analyses of halophyte rice *Oryza coarctata*… *Physiologia Plantarum*, 173(4), 1309–1322.        | Draft genome + reused/extended RNA-seq (GSE44913), small RNA (168 miRNAs), WGBS                   | 10.1111/ppl.13284            | PRJNA598408; PRJNA656631 (smRNA); PRJNA656632 (bisulfite); portal [ccbb.jnu.ac.in/ory-coar](http://ccbb.jnu.ac.in/ory-coar) | First genome-anchored expression + methylation resource. Methylation data lets you check if OcMT promoter CpG state tracks expression.        |
| Zhao, H., Wang, W., Yang, Y., … Zhang, Z. (2023). A high-quality chromosome-level wild rice genome of *Oryza coarctata*. *Scientific Data*, 10, 701.                                                 | HiFi + Hi-C genome (KKLL, 24 chr) + bulk RNA-seq (13.23 Gb, pooled root/stem/leaf) for annotation | 10.1038/s41597-023-02594-1   | SRA — BioProject not resolved here; confirm via data-availability section                                                   | **The reference genome to annotate against.** RNA-seq is pooled tissue — no cell-type or even organ-level signal.                             |
| Fornasiero, A., Feng, T., Al-Bader, N., et al. (2025). *Oryza* genome evolution through a tetraploid lens. *Nature Genetics*, 57(5), 1287–1297.                                                      | Pan-*Oryza* genome/RNA-seq; coarctata included among 11 wild species                              | 10.1038/s41588-025-02183-5   | [PRJNA439330](https://ncbi.nlm.nih.gov/bioproject/PRJNA439330)                                                              | Best resource for cross-species orthology and homoeolog resolution — directly relevant to the KK/LL subgenome question.                       |
| Tasnim, A., Jahan, I., Azim, T., Karmoker, D., & Seraj, Z. I. (2023). Paired growth of cultivated and halophytic wild rice under salt stress… *Frontiers in Plant Science*, 14, 1244743.             | Bulk mRNA-seq, *O. sativa* (BRRI Dhan 67) leaves, paired vs. unpaired with coarctata, ± salt      | 10.3389/fpls.2023.1244743    | In Supplementary Material — not resolved here                                                                               | RNA-seq is on the *O. sativa* side of the pairing, not coarctata itself.                                                                      |

**Excluded:** Mondal et al. (2017, F1000Research, 10.12688/f1000research.12414.2) and Mondal et al. (2018, *Sci Rep*, 10.1038/s41598-018-31518-y) — genome assembly papers using DNA-seq, not independent RNA-seq experiments. Tamanna et al. (2024, 10.1002/pei3.10155) — metabolomics, not transcriptomics.

## Complete inventory by data type

| Data type | Exists? | Top dataset | Accession / DOI |
|---|---|---|---|
| Genome (DNA-seq) | Yes, 3 versions | Zhao et al. (2023) — HiFi + Hi-C, 24 chr, 45,571 genes. **Use this one.** | 10.1038/s41597-023-02594-1 |
| | | Mondal et al. (2018) — older, fragmented, superseded | 10.1038/s41598-018-31518-y |
| RNA-seq (bulk mRNA) | Yes, condition-resolved (one study) | Garg et al. (2014) — control/salt450/salt700/submergence | GSE44913 |
| Small RNA / miRNA | Yes | Mondal, Ganie, & Debnath (2015) — control vs. salt450, leaf | PRJNA271658 |
| Epigenome (WGBS) | Yes, one study | Bansal et al. (2021) — 19–48% methylcytosine across contexts | PRJNA656632 |
| Metabolome | Yes, one study | Tamanna et al. (2024) — root, untargeted, sativa vs. coarctata | 10.1002/pei3.10155 |
| Proteome | Yes, one study | Sengupta & Majumder (2010) — leaf 2D-gel + MALDI-TOF, >700 spots | 10.1007/s00425-008-0878-y |
| Microsatellite / SSR | Yes | Dalai et al. (2021) — core STS marker set | See Mondal 2018 (230,968 SSR list) |
| Cytogenetic / ploidy | Yes | Chowrasia et al. (2021) — revised to triploid (2n=3x=36) | 10.1016/j.plantsci.2021.110878 |
| Endophyte / microbiome | Yes | Tasnim et al. (2023) | 10.3389/fpls.2023.1244743 |
| **Single-cell (any omics)** | **No** | — none exists | — |
| **Spatial transcriptomics** | **No** | — none exists | — |
| **Multi-organ replicated bulk RNA-seq** | **No** | Existing RNA-seq is pooled-tissue or single-condition | — |

## Top 2 to start with

1. **Zhao et al. (2023)**, *Scientific Data* — the reference genome. Orthology, remapping, promoter coordinates, and MT gene models all depend on it.
2. **Garg et al. (2014)**, *DNA Research* (GSE44913) — the only condition-resolved expression data (salt/submergence). Remap this onto #1.

## Related

- [[Oryza sativa scRNA-seq datasets]]
- [[Ortholog projection strategy]]
- [[2026-08-20]]
