---
type: note
project: "[[03_adenocarcenoma_single_cell_moc]]"
status: active
tags:
  - single-cell
  - methods
  - star-methods
---

## STAR★Methods

## Legend
- <mark style="background: red;">Red</mark> — Problem
- <mark style="background: green;">Green</mark> — Solution
- <mark style="background: blue;">Blue</mark> — Methods
- <mark style="background: cyan;">Cyan</mark> — Data/numbers
- <mark style="background: yellow;">Yellow</mark> — Description/background
- <mark style="background: purple;">Purple</mark> — Future application/direction
- <u>Underline</u> — Limitation
- [[Backlink]] — Unfamiliar term

---

### Key resources table

|REAGENT or RESOURCE|SOURCE|IDENTIFIER|
|---|---|---|
|**Biological samples**|   |   |
|Pediatric patient tumor tissue|This paper, UZ Ghent|ss|
|**Chemicals**, **peptides**, **and recombinant proteins**|   |   |
|b-mercaptoethanol|Sigma-Aldrich|Cat# M3148|
|Collagenase A|Sigma-Aldrich|Cat# 11088793001|
|DAPI|Invitrogen|Cat# D1306; RIDD: AB_2629482|
|DMSO|Fisher Scientific|Cat# 10103483|
|Dnase I|Sigma-Aldrich|Cat# 04 536 282 001|
|EDTA|Westburg|Cat# 51234|
|FcBlock 2.4G2|Bioceros|N/A|
|FCS|Merck Life Science|Cat# F0804|
|Fixable Viability due Live/Dead - eFluor780|eBioscience|Cat# 65-0865-18|
|RPMI 1640|Gibco|Cat# 52400-025|
|RBC lysis buffer|BioLegend|Cat# 420302|
|**Deposited data**|   |   |
|Manuscript code|This study|[https://github.com/VIBTOBIlab/NBAtlas_manuscript](https://github.com/VIBTOBIlab/NBAtlas_manuscript)|
|In-house data|This study|GEO: [GSE253865](http://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE253865)|
|In-house data|This study|EGA: EGAD50000000328|
|NBAtlas reference atlas data|This study|Mendeley Data: [https://doi.org/10.17632/yhcf6787yp.1](https://doi.org/10.17632/yhcf6787yp.1)|
|NBAtlas reference atlas visualization|This study|R2 platform: [https://hgserver2.amc.nl/cgi-bin/r2/main.cgi?dscope=NBSCA&option=about_dscope](https://hgserver2.amc.nl/cgi-bin/r2/main.cgi?dscope=NBSCA&option=about_dscope)|
|NBAtlas reference atlas visualization|This study|[https://single-cell.be/nbatlas/](https://single-cell.be/nbatlas/)|
|**Software and algorithms**|   |   |
|AUCell (v1.20.2)|Aibar et al.[59](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib57)|[https://www.bioconductor.org/packages/release/bioc/html/AUCell.html](https://www.bioconductor.org/packages/release/bioc/html/AUCell.html)|
|CellRanger (v6.1.2)|10x Genomics|[http://www.10xgenomics.com](http://www.10xgenomics.com/)|
|ClusterProfiler (v4.4.4)|Wu et al.[115](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib118)|[https://bioconductor.org/packages/release/bioc/html/clusterProfiler.html](https://bioconductor.org/packages/release/bioc/html/clusterProfiler.html)|
|CopyKAT (v1.1.0)|Gao et al.[116](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib119)|[https://github.com/navinlabcode/copykat](https://github.com/navinlabcode/copykat)|
|FastCAR (v0.1.0)|Berg et al.[117](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib120)|[https://github.com/LungCellAtlas/FastCAR](https://github.com/LungCellAtlas/FastCAR)|
|fgsea (v1.22.0)|ss|[https://bioconductor.org/packages/release/bioc/html/fgsea.html](https://bioconductor.org/packages/release/bioc/html/fgsea.html)|
|ggplot2|ss|[https://cran.r-project.org/web/packages/ggplot2/](https://cran.r-project.org/web/packages/ggplot2/)|
|Harmony (v0.1.0)|Korsunsky et al.[36](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib36)|[https://github.com/immunogenomics/harmony](https://github.com/immunogenomics/harmony)|
|infercnvpy (v0.4.2)|ss|[https://github.com/icbi-lab/infercnvpy](https://github.com/icbi-lab/infercnvpy)|
|NMF (v0.24.0)|ss|[https://cran.r-project.org/web/packages/NMF](https://cran.r-project.org/web/packages/NMF)|
|scanpy (v1.8.1)|Wolf et al.[118](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib121)|[https://github.com/scverse/scanpy](https://github.com/scverse/scanpy)|
|scDblFinder (v1.10.0)|Germain et al.[119](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib122)|[https://github.com/plger/scDblFinder](https://github.com/plger/scDblFinder)|
|SCEVAN (v1.0.1)|De Falco et al.[38](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib38)|[https://github.com/AntonioDeFalco/SCEVAN](https://github.com/AntonioDeFalco/SCEVAN)|
|scvi-tools (v0.16.4)|Gayoso et al.[34](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib34)|[https://github.com/scverse/scvi-tools](https://github.com/scverse/scvi-tools)|
|Seurat (v4.1.0)|Stuart et al.,[120](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib123) Hao et al.[121](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib124)|[https://github.com/satijalab/seurat](https://github.com/satijalab/seurat)|
|SingleR (v1.10.0)|Aran et al.[122](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib125)|[https://github.com/dviraran/SingleR](https://github.com/dviraran/SingleR)|
|UCell (v2.0.1)|Andreatta et al.[58](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib56)|[https://github.com/carmonalab/UCell](https://github.com/carmonalab/UCell)|
|**Other**|   |   |
|Dong et al. (2020) tumor dataset|Dong et al.[15](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib15)|GEO: [GSE137804](http://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE137804)|
|Kildisiute et al. (2021) tumor dataset|Kildisiute et al.[17](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib17)|[https://www.neuroblastomacellatlas.org/](https://www.neuroblastomacellatlas.org/)|
|Slyper et al. (2020) tumor dataset|Slyper et al.[19](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib19)|GEO: [GSE140819](http://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE140819)|
|Verhoeven et al. (2022) tumor dataset|Verhoeven et al.[20](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib20)|GEO: [GSE147766](http://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE147766)|
|Jansky et al. (2021) fetal adrenal medulla dataset|Jansky et al.[16](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib16)|[https://adrenal.kitz-heidelberg.de/developmental_programs_NB_viz/](https://adrenal.kitz-heidelberg.de/developmental_programs_NB_viz/)|
|Van Haver et al. (2024) iPSC dataset|Van Haver et al.[45](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib45)|GEO: [GSE211661](http://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE211661)|
|SEQC cohort dataset|SEQC consortium[67](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib68)|GEO: [GSE62564](http://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE62564)|
|NRC cohort dataset|NRC consortium[48](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib59)|GEO: [GSE85047](http://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE85047)|

### Experimental model and subject participant details

<mark style="background: yellow;">All [[03_adenocarcenoma_single_cell_neuroblastoma_notes]] patient samples were collected as residual material after both diagnostic workups and after acquiring informed consent from the patient’s guardian, in accordance with the Ethical Committee of UZ Ghent (EC number 2019/1428).</mark> For further details, see [Table S1](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#mmc2).

### Method details

#### Processing of published data into the NBAtlas

##### Data collection

For the construction of the NBAtlas, only samples confirmed to be human neuroblastoma samples (based on the clinical metadata provided) were included. Samples of [[ganglioneuroma]], [[ganglioneuroblastoma]], [[PDX]], mouse, cell line, etc. were excluded. For one dataset (Dong et al. 2020[15](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib15)), raw sequencing files ([[FASTQs]]) were available and were processed into count tables using [[CellRanger]] (v6.1.2) aligned to [[GRCh38.99]]. [[FastCAR]][117](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib120) (v0.1.0) was used to limit [[ambient RNA]] using the CellRanger web summary to determine the ‘emptyDropletCutoff’ (other parameters were default), as described in.[69](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib85) For the other datasets,[16](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib16),[17](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib17),[18](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib18),[19](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib19),[20](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib20) count tables were downloaded from data repositories (e.g., GEO) or sent by the corresponding author. If available, unfiltered count tables were preferred over filtered count tables.

##### Patient metadata

Metadata was collected from the different publications or provided by the original authors and compiled. For most samples, [[INSS]] or [[INRG]] stage, *[[MYCN]]* amplification status, [[CNA]] profile, etc. was available, as reported by the authors (see [Table S1](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#mmc2)). For one sample (Verhoeven2022_NB37), _MYCN_-amplification classification was based on an extremely high (>98th quantile) MYCN expression in a large number of tumor cells (as also discussed with the authors, personal communication).

##### Risk classification

Since studies included in the NBAtlas used different risk-classification systems (COG, NB2004, INRG or not mentioned which one), we uniformly revised the risk status for each sample. High-risk samples were distinguished from low/intermediate samples if they originated from a patient with INSS 4/INRGSS M, _MYCN_ amplification, or a segmental CNA profile. The remaining samples (i.e., with another INSS/INRGSS class, no _MYCN_ amplification, and no segmental CNA profile) were classified as low/intermediate-risk.

##### Data quality control

To filter out remaining low-quality cells, a homogeneous filter of minimally 200 genes, minimally 500 counts, and maximally 10% or 25% mitochondrial reads, for single-nucleus or single-cell samples, respectively, was applied. To filter out remaining [[doublets]], the current best-performing method-[[scDblFinder]] (v1.10.0) was used[56](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib53),[119](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib122) (run per sample with default parameters and cluster = ‘seurat_clusters’). Gene names from different datasets were updated and made unique using the R package HGNChelper (v0.8.1).[123](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib126) After merging the different datasets, genes with nonzero counts in minimally 10 cells were retained.

##### Data integration

After merging the count data of all samples, standard pre-processing, and normalization using the scanpy[118](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib121) (v1.8.1) pipeline was performed (the top 5000 highly variable genes were retained for further analyses). <mark style="background: blue;">To correct for [[batch effects]], the [[scVI]] algorithm[35](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib35) was used (scvi-tools python package v0.16.4, with ‘sample’ as the covariate, n_layers = 2, encode_covariates = True, use_layer_norm = ’both’, use_batch_norm = ’none’).</mark> The scVI model was trained with ‘max_epochs = 500’ (and early_stopping = True). Thereafter, the latent representation provided by scVI was used as input to generate a [[UMAP]] (using scanpy.pp.neighbors with n_pcs = 15 and n_neighbors = 20, followed by scanpy.tl.umap with min_dist = 0.6). Clustering was performed with scanpy.tl.[[leiden]]. Integration with [[Harmony]][36](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib36) was also performed (with ‘sample’ as the covariate) and showed highly similar results in terms of cell clustering, however, the immune cells were not as clearly separated from the neuroendocrine cells and we therefore proceeded with the scVI integration results.

##### Cell type annotation

Cell types were annotated using canonical markers and differentially expressed (DE) genes (as indicated in the dot plot in [Figure 1](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#fig1)D). A cluster of cells coming from samples with adrenal [cortex cells](https://www.sciencedirect.com/topics/biochemistry-genetics-and-molecular-biology/cell-cortex) (and a few liver cells, based on _ASGR1_ and _ALB_ expression), mainly from samples Slyper2020_nucleus_HTAPP-244-SMP-451_TST and Jansky2021_NB02, respectively, was annotated as ‘stromal other’. DE genes were calculated using the FindMarkers function (Seurat[121](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib124) v4.1.1 package) per cluster or cell type (with min.diff.pct = 0.3, logfc.threshold = 0.3). DE genes were ranked based on a specificity score, defined for each gene as the average log2 fold-change multiplied by the percentage of cells in the cluster expressing this gene over the percentage expressed in other cells.

##### Copy number inference

For inference of CNAs, all cell types except for potential CNA-bearing cells, i.e., neuroendocrine, fibroblast, and Schwann cells, were included as reference cells. Infercnvpy (v0.4.2) was used to infer CNAs from the normalized counts (with window_size = 250 and step = 1). Genomic positions of the genes were annotated with infercnvpy.io.genomic_position_from_gtf using the GENCODE v43 gene annotation. Cells were clustered according to CNA profiles (using infercnvpy.tl.pca, infercnvpy.pp.neighbors, and infercnvpy.tl.leiden with default parameters) and CNA scores (genome-wide) were calculated with infercnvpy.tl.cnv_score (with default parameters). To calculate CNA scores for chromosomes or [chromosome arms](https://www.sciencedirect.com/topics/neuroscience/chromosome-arm), the infercnvpy.tl.cnv_score function was used after infercnvpy was rerun per study and results were merged to minimize batch effects.

To confirm the [[infercnvpy]] results, we also used [[CopyKAT]] (v1.1.0)[116](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib119) and [[SCEVAN]] (v1.0.1).[38](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib38) Classification of [[aneuploid]]/tumor vs. [[diploid]]/normal cells was performed on a per-sample basis to exclude potential batch effects at classification. As for infercnvpy, all cell types except for neuroendocrine, fibroblast, and Schwann cells were used as reference cells. Providing a good baseline reference has been shown to drastically improve the confident classification performance.[116](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib119) <u>To ensure this, only samples with at least 100 reference cells were classified (other samples were labeled ‘not.run’).</u>

##### Reference-based mapping to normal sympathoadrenal development

Reference mapping of neuroendocrine cells to a fetal [adrenal medulla](https://www.sciencedirect.com/topics/neuroscience/adrenal-medulla) dataset (from Jansky et al. 2021[16](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib16)) and human induced pluripotent stem cell (iPSC) model of sympathoadrenal development (from Van Haver et al. 2024[45](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib45)) was performed with SingleR[122](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib125) (v1.10.0, default parameters) based on Spearman correlation or Seurat (using the FindTransferAnchors and TransferData functions with default parameters). Log-normalized counts were used as input for both the reference and query data.

##### Gene signature scoring

To calculate gene signature scores and to be able to compare different signatures in the same cells, the UCell[58](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib56) (v2.0.1) method was used. To calculate multiple UCell signature scores at once, the enrichIt function (R escape package, v1.6.0) was used. [Cell cycle phase](https://www.sciencedirect.com/topics/neuroscience/cell-cycle-phase) assignment was performed using the CellCycleScoring function (Seurat v4.1.1 package).

#### Tumor and immune zoom

##### Tumor zoom

Neuroendocrine cells classified as aneuploid cells by CopyKAT were selected for the malignant tumor zoom. Integration was performed again after standard scanpy preprocessing as described above (now with updated top 5000 highly variable genes). scVI integration was performed with the same parameters as above. Leiden clustering was performed (with a resolution of 0.5). <u>We also tried Harmony for integration (with sample alone or sample and assay as the covariate) but this provided insufficient integration of single-cells and single-nuclei (because of the assay-specific expression of the top genes used for integration). Furthermore, we tried correcting for cell cycle but this removed most DE genes indicating a loss of biological heterogeneity and we thus abandoned this approach.</u> Seurat integration[120](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib123) of the samples was run with the RPCA algorithm. ComBat integration[124](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib127) was run with default parameters (using scanpy.pp.combat with ‘samples’ as batch key). DE genes were calculated as described above (with default cutoffs). [Gene set enrichment analysis](https://www.sciencedirect.com/topics/biochemistry-genetics-and-molecular-biology/gene-set-enrichment-analysis) (GSEA) was performed per cluster using the fgsea R package (v1.22.0) with a ranking based on the specificity score for all genes (see above) with Reactome 2022 and ChEA2022 gene sets. Only GSEA results with an FDR below 0.1 were visualized.

##### NMF program detection

[[Non-negative matrix factorization]] (NMF) programs in malignant cells were determined as described by Gavish et al.[47](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib54) To account for batch effects, NMF was run for each sample separately using the NMF R library (v0.24.0). Only samples with 10 malignant cells were considered, as recommended by Gavish et al.[47](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib54) [[Metaprograms]] (MPs) were determined by clustering the reoccurring NMF programs by [[Jaccard similarity]]. MP-defining genes (or signatures) were derived by selecting the top 50 most recurring genes per metaprogram. MPs were investigated to represent not just one study (dataset). This was not the case for any MP.

NMF overrepresentation analysis was performed using the enricher function (clusterProfiler[115](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib118) R package v4.4.4) with the following gene sets: Hallmark genesets, C6 genesets, Reactome downloaded from MSigDB ([https://www.gsea-msigdb.org/gsea/msigdb/](https://www.gsea-msigdb.org/gsea/msigdb/)) as well as a collection of signatures from different studies.[16](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib16),[21](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib21),[44](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib44),[46](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib61),[47](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib54),[66](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib67)

##### Metaprogram survival analysis

<mark style="background: cyan;">Survival analysis of [[MP]] signatures was performed using the SEQC cohort bulk RNA-seq data (_n_ = 498 samples, GEO accession: [GSE49710](http://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE49710)) and NRC cohort [microarray](https://www.sciencedirect.com/topics/neuroscience/microarrays) data (n = 276 samples, GEO accession: [GSE85047](http://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE85047)).</mark> [[Kaplan-Meier]] curves were calculated using overall survival for high vs. low (log2) expression of the MP signatures (highest quartile cutoff) using the survival R package (v3.5-7) package. _p_ values were calculated with a [[log-rank test]].

##### Gene signature scoring

The UCell (as described above) and AUCell (v1.20.2)[59](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib57) signature scoring was performed with default parameters. For the UCell van Groningen et al. mesenchymal gene signature, the threshold was determined manually based on the expression in immune cells (used as background). For AUCell, the threshold was determined automatically (with inspection of the thresholds).

##### Immune zoom

Immune cell types ([[myeloid]], B cell, plasma, [[pDC]], T cell, and [[NK cell]]) were selected from the entire atlas and reintegrated using the same scVI-pipeline as described above. Clustering was performed with the Leiden algorithm (with a resolution of 1). Low-quality cells clustering separately and/or co-expressing markers of non-immune populations were removed. DE genes were calculated as described above with FindMarkers (with default cutoffs).

##### Monocyte/macrophage zoom

Monocytes and macrophages were selected from the immune zoom for realignment across the samples. Given the reduced number of cells/nuclei (_n_ = 14,860) the integration was performed using Harmony (v0.1.0) instead of the scVI-pipeline.[36](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib36),[56](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib53) Another round of quality control was performed here to eliminate remaining doublets or low-quality cells/nuclei. DE gene calculation was performed in the same way as for the immune zoom.

#### In-house generated single-cell and single-nucleus RNA-seq data

##### Patient samples

Samples were transported in RPMI and on ice where possible. Samples were either processed fresh or first viably frozen (in a solution of 10% DMSO, 50% FCS, and 40% RPMI) or snap-frozen (no medium) before proceeding to the isolation of single cells or nuclei.

##### Isolation of single neuroblastoma cells

Single-cell isolation was performed as described in Guilliams et al. 2022.[69](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib85) In short, tumor specimens were minced into small pieces and digested into single-cell suspensions using 1 mg/mL [Collagenase](https://www.sciencedirect.com/topics/biochemistry-genetics-and-molecular-biology/collagenase) A (Sigma-Aldrich) and 10 U/mL DNAse I (Sigma-Aldrich) in RPMI at 37°C for a maximum of 30 min with agitation until the tissue was digested. Next, cells were pelleted by [centrifugation](https://www.sciencedirect.com/topics/biochemistry-genetics-and-molecular-biology/centrifugation) (5 min at 400 g). Red [blood cell](https://www.sciencedirect.com/topics/neuroscience/hemocyte) lysis was performed when required by incubating the cells with RBC [lysis buffer](https://www.sciencedirect.com/topics/neuroscience/lysis-buffer) (BioLegend) for 3 min followed by a wash step. For [[CITE-seq]], an [Fc receptor](https://www.sciencedirect.com/topics/neuroscience/fc-receptor) block 2.4G2 (Bioceros) was added together with CITE-seq antibodies (BioLegend; antibody details described in Guilliams et al. 2022[69](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib85)). Following 20 min of incubation at 4°C, the cells were washed with PBS with 2% FCS and 2mM EDTA. For regular single-cell RNA-seq, this step was omitted. Cells were then stained with a live-dead discrimination dye (Live/Dead eFluor780, eBioscience) by incubating the cells for 15 min at 4°C followed by a wash step. Approximately 160,000 live cells were then [[FACS-purified]] per sample (using BD FACSAria III). After sorting, cells were pelleted by centrifugation at (5 min at 400 g).

##### Isolation of single neuroblastoma nuclei

Nuclei were isolated from snap-frozen tumor tissue as described in Guilliams et al. 2022[69](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib85) and Habib et al. 2016.[125](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib128) Briefly, snap or viably frozen neuroblastoma tissues were [[dounce homogenized]] in a homogenization buffer. The homogenate was filtered over a 70 μm cell strainer. Next, the nuclei were pelleted using a [sucrose](https://www.sciencedirect.com/topics/biochemistry-genetics-and-molecular-biology/sucrose) [density gradient ultracentrifugation](https://www.sciencedirect.com/topics/biochemistry-genetics-and-molecular-biology/density-gradient-centrifugation) (7,700 rpm for 30 min at 4°C). After resuspension, nuclei were stained with [DAPI](https://www.sciencedirect.com/topics/neuroscience/differential-attentional-process-inventory) (Invitrogen) and incubated for 5 min, and 100,000 to 400,000 intact nuclei were FACS-purified from remaining debris (using BD FACSAria III). Purified nuclei were pelleted by centrifugation, first for 3 min at 400 g and subsequently for 5 min at 600 g.

##### Single-cell or single-nucleus RNA-sequencing

After centrifugation, cells or nuclei were resuspended in 18.5 μL in PBS with 0.04% [BSA](https://www.sciencedirect.com/topics/neuroscience/bovine-serum-albumin). 2 μL of this solution was used to calculate the concentration of cells or nuclei after flow cytometric counting. 20,000 cells or nuclei were loaded onto a Chromium (10X Genomics) controller. Single-cell or single-nucleus libraries were generated using the Chromium Single Cell 3 (V2 or V3) Reagent Kit according to the manufacturer’s protocol. Libraries were sequenced using an Illumina NovaSeq 6000 sequencing platform.

##### Matching single-cell and single-nucleus RNA-sequencing data processing

For matching single-cell and single-nucleus data generation, we used four parts from one tumor and split each part into two pieces for matching CITE-seq and single-nucleus RNA-seq with two technical replicates each (i.e., CITE-seq: Bonine2023_cell_CS202-209 and single-nucleus RNA-seq: Bonine2023_nucleus_CS210-217). Data processing of the matching single-cell and single-nucleus RNA-seq data was performed similarly to that described above, using CellRanger (for single-nucleus data processing, the option include-introns = T was added) and FastCAR. Cells with at least 200 and less than 8,000 genes, less than 60,000 counts, and less than 40% mitochondrial reads were kept. Additionally, when merging the data of different samples, only genes with counts for at least three cells were retained. Preprocessing was done using the standard pre-processing and normalization scanpy pipeline. Different single-nuclei samples and CITE-seq samples were integrated using the [[TotalVI]] model[126](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib129) (v0.6.7, using the top 4000 most highly variable genes, according to the workflow described on [scvi-tools.org](http://scvi-tools.org/)). Subsequently, [[Louvain]] clustering was performed in the TotalVI [[latent space]]. The antibody ([[ADT]]) counts from CITE-seq data were further not considered. Clusters with a decreased number of genes, increased percentage of mitochondrial reads, and/or expressing markers of multiple cell types were removed. Cell-type annotation was performed as described above.

##### In-house data for mapping to the NBAtlas

In-house single-cell and single-nucleus RNA-seq data from six patients, with one having matched data (see [Table S1](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#mmc2)), was included for mapping to the NBAtlas. All samples were individually pre-processed and quality control was performed with the same procedure as described above for the NBAtlas. Manual annotation was performed for each sample following log-normalization and UMAP generation (with a standard Seurat pipeline) using the top markers from the NBAtlas.

##### scArches data integration and cell type prediction

<mark style="background: blue;">For the integration of in-house data with the NBAtlas, the [[scANVI]]-[[scArches]] pipeline was used.</mark> To exploit the biological knowledge already embedded in the atlas as cell type annotation, the scVI model was first further trained on the cell type labels with scANVI[127](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib130) (scvi-tools package v0.16.4, with n_layers = 4, max_epochs = 500, early_stopping = ’True’). This was then used as input for scArches model training (v0.5.6, max_epochs = 500) of the query data. scANVI-scArches cell type prediction was performed with an uncertainty of 0.5 (as recommended by the authors[30](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib30)). To obtain an integrated atlas of the query and reference atlas, a UMAP was generated in the scArches latent space. After the scArches integration, another round of quality control was performed. A cluster of doublets (co-expressing markers of different cell types), remaining in the in-house data was removed.

##### SingleR cell type prediction

SingleR[122](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib125) (v1.10.0) cell type prediction of in-house data with the NBAtlas as a reference was run as described above (with default parameters). Ribosomal and [mitochondrial genes](https://www.sciencedirect.com/topics/neuroscience/mitochondrial-gene) were removed from the reference to avoid these being selected as genes for mapping. For visualization of the results of the query together with the reference data, we used the scArches UMAP.

#### Visualization

UMAPs were plotted with the Seurat (v4.1.1) or plot1cell (v0.0.1) package. Feature plots were created using ordered normalized expression using the FeaturePlot function (Seurat package) with a quantile cutoff of 0.02–0.98. Dot plots were generated with the DotPlot function (Seurat package) or with ggplot2. Other figures were created with ggplot2. Some icons were generated with Biorender.

### Quantification and statistical analysis

For statistical comparison of means between two non-normally distributed unpaired conditions, the [Wilcoxon test](https://www.sciencedirect.com/topics/biochemistry-genetics-and-molecular-biology/mann-whitney-u-test) was used. [[Differential abundance]] testing was performed with the [[edgeR]] package ([[glmQLFTest]] function).[128](https://www.sciencedirect.com/science/article/pii/S2211124724011550?via%3Dihub#bib131) For correlation analysis, [[Kendall’s rank]] correlation test was used. For survival analysis, the log rank test was used. For multiple testing, [[Benjamini-Hochberg]] correction was used.
