---
type: paper
status: active
citekey: Usman2025
year: 2025
authors:
  - Babar Usman
  - Naveed Khan
  - Yiming Wang
  - Ravi Gupta
  - Soon Wook Kwon
  - Sun Tae Kim
url: https://doi.org/10.1016/j.plantsci.2025.112964
date: 2026-08-18
tags:
  - single-cell
  - plant-biology
  - scRNA-seq
  - review
legacy-status: inbox
---
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

## My Ideas

1. scRNA-seq reveals cell-layer-specific responses to abiotic and biotic stresses, and its emerging role in tracing specialized-metabolite production and dissecting mutational effects at single-cell resolution.
   → *Note: this is a good point, can work on this.*
2. scRNA-seq enables precise identification of candidate genes, functionally validated via CRISPR/Cas9-mediated genome editing to enhance specific traits.
3. Protoplast isolation is a key technical bottleneck for plant scRNA-seq.
   → *Note: I will do this for coarctata rice.*

## Abstract

<mark style="background: yellow;">Single-cell RNA sequencing ([[scRNA-seq]]) has brought a significant shift in our ability to dissect plant [[cellular heterogeneity]] and developmental processes with unprecedented resolution.</mark> <mark style="background: red;">However, its integration with [[functional genomics]] and [[spatial transcriptomics|spatial technologies]] in plant systems remains limited, leaving critical gaps in our understanding of gene regulation, stress responses, and [[cell fate]] decisions.</mark> <mark style="background: blue;">In this review, we provide a comprehensive synthesis of scRNA-seq applications across diverse plant tissues, illustrating how these datasets have uncovered [[developmental trajectories]], [[lineage dynamics]], and cell-type-specific transcriptional programs.</mark> We further highlight how scRNA-seq has revealed cell-layer-specific responses to [[abiotic stress|abiotic]] and [[biotic stress|biotic]] stresses, and its emerging role in tracing the production of [[specialized metabolites]] and dissecting mutational effects at single-cell resolution. <mark style="background: green;">Notably, we highlight how scRNA-seq enables the precise identification of candidate genes, which have been functionally validated through [[CRISPR/Cas9]]-mediated genome editing to enhance specific traits.</mark> <mark style="background: purple;">We also explore recent advances in [[spatial transcriptomics]] and emerging [[multi-omics]] approaches that combine transcriptomic data with [[chromatin accessibility]] or protein expression.</mark> Uniquely, our review integrates insights across plant species and tissue types, offering a cross-cutting perspective on plant development and adaptation. <u>Finally, we critically evaluate key technical challenges, such as [[protoplast isolation]], limited [[marker gene]] availability, and [[cell-type annotation]], and propose potential solutions.</u> Collectively, this review offers a timely overview of how single-cell and spatial transcriptomics have advanced gene discovery and trait improvement by enabling high-resolution insights into plant tissue development and stress responses.

## Introduction
 
Organisms comprise cells with diverse morphologies and specialized functions, and gene expression patterns vary across cell types, driving [[differentiation]] and enabling distinct biological roles (Arendt et al., 2016). Advances in [[single-cell omics]] now allow unprecedented resolution of cell-type-specific gene expression, revealing programs that shape [[cellular identity]]. By profiling discrete cell populations during development and [[homeostasis]], we can define the [[regulatory networks]] that direct cell identity in space and time (Wang et al., 2023a). This knowledge clarifies how specialized cells emerge and coordinate to build complex tissues.

Transcriptomics or RNA-sequencing (RNA-seq) enables high-throughput analysis of protein-coding and non-coding RNAs in tissues or cells (Wang et al., 2009). [[Bulk RNA-seq]] has been widely used to study global gene expression across tissues for over three decades (Tyagi et al., 2022), but resulting in average expressions that mask cellular heterogeneity. <mark style="background: red;">Because individual cells exhibit substantial variability in gene expression and regulation (Rosenfeld et al., 2005), whole-tissue transcriptomics limits the ability to resolve cell-type-specific networks, [[rare cell populations]], and developmental transitions (Shaw et al., 2021).</mark> Single-cell analysis is therefore essential for capturing fine-scale gene expression dynamics that underline tissue structure and function.

Single-cell RNA sequencing (scRNA-seq) profiles transcriptomes at single-cell resolution, distinguishing cell types based on high-throughput expression profiles and enabling reconstruction of developmental trajectories (Efroni and Birnbaum, 2016). Therefore, scRNA-seq can unveil regulatory networks governing cellular differentiation and tissue development by [[delineating]] transcriptional differences between discrete cell populations. <mark style="background: blue;">This review summarizes key principles of plant scRNA-seq, from experimental design to computational analysis and highlights emerging applications across species.</mark> In recent years, single-cell transcriptome maps have been progressively applied to model plant species such as [[Arabidopsis]] (Zhang et al., 2019a) and [[Medicago]] (Cervantes-Pérez et al., 2022) as well as agronomically important crops, including rice ([[Liu et al., 2021]]a, [[Wang et al., 2021]]), corn (Xu et al., 2021a), sorghum (Fu et al., 2024), cotton (Qin et al., 2022), strawberry (Bai et al., 2022), tomato (Omary et al., 2022), tea tree (Wang et al., 2022), soybean (Sun et al., 2023a) and many additional species to study the genetic regulation of plant development (Cho et al., 2025).

