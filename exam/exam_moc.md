---
type: moc
project: exam
status: active
tags:
  - meta
  - exam
  - immunology
  - tumor-immunology
---
# Exam — Map of Content

> [!info] Scope
> Exam-prep notes for tumor immunology and clinical immunology: tumor antigen
> classification, immune surveillance of cancer, NETosis/antitumor activity,
> CAR-T therapy, and immunodeficiency (primary and secondary).
> Mostly lecture-slide screenshots + Excalidraw scratch boards captured live,
> written up into clean notes afterward.

## Core Notes (Written Up)

- [[501 ZM]] — **Tumor Antigens**: old TSA/TAA distinction vs. modern **MOO-VOAC** classification (mutated oncogenes/TSGs, other mutated genes, overexpressed proteins, viral antigens, oncofetal antigens, altered glycolipids/glycoproteins, differentiation antigens); mechanism tables (mutation/inappropriate expression/overexpression → TSTA/TATA); neoantigens; oncogenic-virus antigens (EBV, HPV); reference table of antigens by cancer type. Embeds 7 slide screenshots. Built on top of the [[zm501]] Excalidraw board.
- [[immune_surveillance_breakdown]] — **Immune Surveillance of Cancer**: the classic mouse chemical-carcinogen experiment (excise tumor → irradiate as vaccine → challenge vs. naive control) showing vaccinated mice resist tumor rechallenge. ⚠️ Its 4 image embeds use `images/...` relative paths but the PNGs (`full_diagram.png`, `step1_initial_setup.png`, `step2_vaccinated_path.png`, `step3_control_path.png`) actually sit directly in `exam/`, not an `images/` subfolder — links are broken, fix by dropping the `images/` prefix.
- [[zm02]] — **Tumor Immunology Part 2**: organized study notes from the [[zm501-02mid]] Excalidraw board. Covers **NETosis** (Initiation/Proliferation/Remodelling phases), **Tumor Microenvironment** (immune cell interactions, NK-mediated cytotoxicity, M2 macrophages, MDSC, VEGF, MMP, ROS, NF-κB, TNF/IL-6/IL-10), **Tumor Immune Evasion** (MHC-I loss, T-reg/MDSC, PD-L1/IL-10/TGF-β, BCL2 resistance), and **CAR-T therapy** (what it is, mechanism, composition). Embeds ~80 slide screenshots.
- [[zm501-03mid]] — **Immunodeficiency – Complete Study Guide**: comprehensive coverage of primary (congenital) and secondary (acquired) immunodeficiencies. Includes: CGD (NADPH oxidase defect, IFN-γ therapy), LAD I/II/III (CD18, GDP-fucose transporter, Kindlin-3), Chédiak-Higashi (LYST mutation), SCID (defective thymic development, nucleotide salvage, cytokine signaling, V(D)J recombination), DiGeorge syndrome, antibody deficiencies (agammaglobulinemia, hyper-IgM), secondary causes (malnutrition, cancer, iatrogenic, HIV), HIV life cycle and pathogenesis, and mermaid diagrams for all major concepts.

## Excalidraw Boards (Raw Capture)

- [[zm501]] — source board behind [[501 ZM]]; live-lecture text elements on tumor antigen classification (TSTA/TATA, MOO-VOAC, oncofetal antigens, MUC-1, immunosurveillance) plus the same 7 embedded slide screenshots — several extra images not yet pulled into a written note (`...162611`, `...163501`, `...163652`, `...163840`, `...164458`, `...164548`, `...164607`, `...164921`, `...165705`).
- [[zm501-02mid]] — source board behind [[zm02]]; live-lecture text elements on NETosis, antitumor activity, tumor microenvironment, CAR-T, plus ~80 embedded slide screenshots (including BMB-507 Tumor Immunology Part 2 slides 65–90). Now written up into [[zm02]].

## Everything in this project (auto)

```dataview
TABLE file.mtime AS Touched
FROM "exam"
WHERE file.name != this.file.name
SORT file.mtime DESC
```

