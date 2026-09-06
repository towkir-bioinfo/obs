---
type: protocol
project: "[[01_homolog_oc_moc]]"
experiment: "[[P001-E001_MT-genome-wide-identification]]"
date: 2026-08-16
tags:
  - homology
  - metallothioneins
  - pipelines
legacy-status: reference
---
# Homolog Analysis Pipeline for *O. coarctata* Metallothionein

## Overview

This document outlines the complete workflow for identifying and characterizing metallothionein homologs in the *O. coarctata* proteome using Pfam profile HMMs and HMMER search tools.

---

## 1. Pfam Profile Download

### Resources
- **Pfam Metallothio_2 Profile**: [PF01439 Logo](https://www.ebi.ac.uk/interpro/entry/pfam/PF01439/logo/)
- **Download Location**: `/home/cblast/towkir/projects/01_homolog_oc/data/raw/PF01439.hmm`

---

## 2. HMMER Search Strategy

| Situation | Tool |
|-----------|------|
| **One/few HMM profiles → search a proteome** | `hmmsearch` |
| **Protein(s) → search against many Pfam HMMs** | `hmmscan` |

---

### HMMER Command

```bash
cd /home/cblast/towkir/projects/01_homolog_oc/data/raw/

hmmsearch --cpu 32 \
  --tblout "/home/cblast/towkir/projects/01_homolog_oc/result/table/PF01439_hits.tbl" \
  "/home/cblast/towkir/projects/01_homolog_oc/data/raw/PF01439.hmm" \
  "/home/cblast/towkir/projects/01_homolog_oc/data/raw/proteinocGWHCBHR00000000.faa" \
  > "/home/cblast/towkir/projects/01_homolog_oc/result/table/PF01439_full.txt"
```

### Domain Table Generation

```bash
hmmsearch \
  --domtblout domtblout.txt \
  PF01439.hmm \
  proteinocGWHCBHR00000000.faa \
  > /dev/null  # Hides massive terminal output
```

---

### Project Directory Structure

```
01_homolog_oc/
├── data/
│   └── raw/
│       ├── PF01439.hmm
│       └── proteinocGWHCBHR00000000.faa
└── result/
    └── table/
        ├── PF01439_hits.tbl
        └── PF01439_full.txt
```

---

## 3. Output File Types

| File | Purpose | Description |
|------|---------|-------------|
| `--tblout hits.tbl` | Protein/hit screening | Significance of target protein matches to HMM |
| `--domtblout domains.tbl` | Domain analysis | Individual HMM domains detected within proteins |

---

## 4. Result Filtering

### Table Format Overview

1. **Target name** → Protein identifier
2. **Accession** → Not present (raw proteome data)
3. **Query name** → Metallothio_2 (Pfam domain)
4. **Accession (query)** → PF01439.24
5. **E-value (full sequence)** → Statistical significance
6. **Score (full sequence)** → Bit score
7. **Bias** → Compositional bias correction

---

### E-value Filtering

**Single value check:**
```bash
awk '!/^#/ && $5 <= 1e-3' PF01439_hits.tbl | wc -l
```

**Multiple value analysis:**
```bash
for e in 0.05 1e-3 1e-5 1e-10; do
  echo "E-value <= $e: $(awk -v e="$e" '!/^#/ && $5 <= e' PF01439_hits.tbl | wc -l)"
done
```

**Results:**
- E-value ≤ 0.05: 20 hits
- E-value ≤ 1e-3: 16 hits
- E-value ≤ 1e-5: 14 hits
- E-value ≤ 1e-10: 13 hits

**Selected cutoff**: E-value ≤ 0.05 (maximal recovery)

---

### Score Filtering (Bit Score)

**HMM cutoff scores from PF01439.hmm:**
```bash
grep -E '^GA |^TC |^NC ' PF01439.hmm
```

**Output:**
- **GA (Gathering)** → 23 23
- **TC (Trusted)** → 23 23  
- **NC (Noise)** → 22.9 22.9

**Score distribution analysis:**
```bash
awk '$0 !~ /^#/ {
  if ($6 >= 20) n20++;
  if ($6 >= 30) n30++;
  if ($6 >= 40) n40++;
  if ($6 >= 50) n50++;
  if ($6 >= 60) n60++;
  if ($6 >= 70) n70++;
  if ($6 >= 80) n80++;
} END {
  print ">=20:", n20
  print ">=30:", n30
  print ">=40:", n40
  print ">=50:", n50
  print ">=60:", n60
  print ">=70:", n70
  print ">=80:", n80
}' PF01439_hits.tbl
```

**Results:**
- ≥20: 17 hits
- ≥30: 14 hits
- ≥40: 13 hits
- ≥50: 13 hits
- ≥60: 13 hits
- ≥70: 12 hits
- ≥80: 6 hits

---

### Bias Filtering

**Important Note**: Metallothionein profiles exhibit strong compositional bias due to high cysteine content. HMMER applies biased-composition correction (null2 model) to account for scores from unusual residue composition.

**Bias percentage calculation**: `(Bias / Bit Score) × 100`

**Bias distribution table:**

| Target Sequence ID | Score | Bias | Bias % | Status |
|--------------------|-------|------|--------|--------|
| GWHPCBHR005103 | 105.0 | 37.6 | 35.81% | ✅ Accept |
| GWHPCBHR066752 | 90.3 | 27.8 | 30.79% | ✅ Accept |
| GWHPCBHR066751 | 89.9 | 28.9 | 32.15% | ✅ Accept |
| GWHPCBHR065072 | 89.8 | 28.3 | 31.51% | ✅ Accept |
| GWHPCBHR065058 | 88.0 | 26.8 | 30.45% | ✅ Accept |
| GWHPCBHR005104 | 80.5 | 14.1 | **17.52%** | ✅ Accept |
| GWHPCBHR063750 | 79.5 | 27.6 | 34.72% | ✅ Accept |
| GWHPCBHR019593 | 78.7 | 25.9 | 32.91% | ✅ Accept |
| GWHPCBHR019591 | 77.8 | 25.9 | 33.29% | ✅ Accept |
| GWHPCBHR065057 | 77.4 | 27.1 | 35.01% | ✅ Accept |
| GWHPCBHR065056 | 75.1 | 31.1 | 41.41% | ⚠️ Borderline |
| GWHPCBHR066753 | 70.6 | 5.8 | **8.22%** | ✅ Accept |
| GWHPCBHR009782 | 66.0 | 49.1 | 74.39% | ❌ Reject |
| GWHPCBHR019592 | 34.2 | 32.4 | 94.74% | ❌ Reject |
| GWHPCBHR004781 | 24.2 | 38.6 | 159.50% | ❌ Reject |
| GWHPCBHR036715 | 22.7 | 9.1 | 40.09% | ⚠️ Borderline |
| GWHPCBHR036714 | 21.0 | 9.4 | 44.76% | ❌ Reject |

---

## 5. Filtering Commands

### Filtered Data Directory
`/home/cblast/towkir/projects/01_homolog_oc/data/filtered/`

### 1. E-value cutoff (≤ 1e-3)
```bash
awk 'BEGIN{OFS="\t"} /^#/ {print; next} $5 <= 1e-3' PF01439_hits.tbl > \
  /home/cblast/towkir/projects/01_homolog_oc/data/filtered/PF01439_evalue_1e-3.tbl
```

### 2. Bit score cutoff (> 23)
```bash
awk 'BEGIN{OFS="\t"} /^#/ {print; next} $6 > 23' PF01439_hits.tbl > \
  /home/cblast/towkir/projects/01_homolog_oc/data/filtered/PF01439_score_over23.tbl
```

### 3. Bias percentage cutoff (≤ 40%)
```bash
awk 'BEGIN{OFS="\t"} /^#/ {print; next} $6 != 0 && ($7/$6)*100 <= 40' PF01439_hits.tbl > \
  /home/cblast/towkir/projects/01_homolog_oc/data/filtered/PF01439_bias_40pct_or_less.tbl
```

### 4. Combined filtering (all three criteria)
```bash
awk 'BEGIN{OFS="\t"} /^#/ {print; next} $5 <= 1e-3 && $6 > 23 && $6 != 0 && ($7/$6)*100 <= 40' PF01439_hits.tbl > \
  /home/cblast/towkir/projects/01_homolog_oc/data/filtered/PF01439_combined.tbl
```

### 5. Counting retained hits
```bash
for f in /home/cblast/towkir/projects/01_homolog_oc/data/filtered/PF01439*.tbl; do
  echo "$(basename "$f"): $(grep -vc '^#' "$f") hits"
done
```

---

## 6. Candidate Protein Extraction

### Extract Candidate IDs
```bash
awk '!/^#/ {print $1}' \
  /home/cblast/towkir/projects/01_homolog_oc/data/filtered/PF01439_combined.tbl \
  | sort -u \
  > /home/cblast/towkir/projects/01_homolog_oc/data/filtered/PF01439_candidate_ids.txt
```

**Candidate IDs extracted:**
```
GWHPCBHR005103
GWHPCBHR005104
GWHPCBHR019591
GWHPCBHR019593
GWHPCBHR063750
GWHPCBHR065057
GWHPCBHR065058
GWHPCBHR065072
GWHPCBHR066751
GWHPCBHR066752
GWHPCBHR066753
```

### Extract Candidate Sequences
```bash
seqkit grep -f \
  data/filtered/PF01439_candidate_ids.txt \
  data/raw/proteinocGWHCBHR00000000.faa \
  > data/filtered/PF01439_candidate_proteins.fasta
```

---

## 7. Candidate Protein Table

| Presentation ID | Original Protein ID | Gene ID | Transcript ID | Length (aa) | Notes |
|-----------------|---------------------|---------|---------------|-------------|-------|
| **OcMT-PF01** | GWHPCBHR005103 | GWHGCBHR003334 | Oco02G001920.1 | 69 aa | MT-like, cysteine-rich |
| **OcMT-PF02** | GWHPCBHR005104 | GWHGCBHR003334 | Oco02G001920.2 | 66 aa | Alternative transcript |
| **OcMT-PF03** | GWHPCBHR019591 | GWHGCBHR012785 | Oco05G010460.1 | 119 aa | Longer protein |
| **OcMT-PF04** | GWHPCBHR019593 | GWHGCBHR012785 | Oco05G010460.3 | 97 aa | Alternative transcript |
| **OcMT-PF05** | GWHPCBHR063750 | GWHGCBHR042392 | Oco22G011490.1 | 64 aa | Strong MT-like architecture |
| **OcMT-PF06** | GWHPCBHR065057 | GWHGCBHR043283 | Oco23G008740.1 | 65 aa | Strong MT-like architecture |
| **OcMT-PF07** | GWHPCBHR065058 | GWHGCBHR043284 | Oco23G008750.1 | 67 aa | Strong MT-like architecture |
| **OcMT-PF08** | GWHPCBHR065072 | GWHGCBHR043298 | Oco23G008890.1 | 66 aa | Strong MT-like architecture |
| **OcMT-PF09** | GWHPCBHR066751 | GWHGCBHR044409 | Oco24G008450.1 | 69 aa | Strong MT-like architecture |
| **OcMT-PF10** | GWHPCBHR066752 | GWHGCBHR044410 | Oco24G008460.1 | 67 aa | Strong MT-like architecture |
| **OcMT-PF11** | GWHPCBHR066753 | GWHGCBHR044410 | Oco24G008460.2 | 47 aa | Alternative transcript/shorter isoform |

---

## 8. Physicochemical Analysis (ProtParam)

### Reference Protein (O. coarctata MT)
- **ID**: WYV70274.1
- **Length**: 64 aa
- **MW**: 6.54 kDa
- **pI**: 5.14
- **Cys**: 10 (15.6%)
- **Instability Index**: 25.82 (stable)
- **Aliphatic Index**: 44.22
- **GRAVY**: -0.470

### Candidate Protein Comparison

| Protein | Length (aa) | MW (kDa) | pI | Cys | Cys % | Instability | Aliphatic | GRAVY |
|---------|-------------|----------|-----|-----|-------|-------------|-----------|-------|
| WYV70274.1 (Reference) | 64 | 6.54 | 5.14 | 10 | 15.6 | 25.82 | 44.22 | -0.470 |
| GWHPCBHR005103 | 82 | 7.84 | 5.13 | 14 | 17.1 | 38.87 | 31.10 | -0.070 |
| GWHPCBHR005104 | 62 | 6.41 | 7.53 | 8 | 12.9 | 56.53 | 55.00 | 0.168 |
| GWHPCBHR063750 | 73 | 7.32 | 5.66 | 12 | 16.4 | 54.95 | 33.56 | -0.322 |
| GWHPCBHR065057 | 74 | 7.27 | 4.90 | 12 | 16.2 | 47.61 | 39.59 | 0.039 |
| GWHPCBHR065058 | 78 | 7.71 | 5.48 | 12 | 15.4 | 42.15 | 37.56 | -0.103 |
| GWHPCBHR066751 | 84 | 8.16 | 4.55 | 12 | 14.3 | 41.13 | 32.62 | -0.076 |
| GWHPCBHR066752 | 78 | 7.60 | 5.50 | 12 | 15.4 | 55.58 | - | - |

**Key Observation**: Candidate GWHPCBHR005103 shows the closest theoretical pI to the reference protein and is predicted to be stable.

---

## 9. Sequence and Domain Analysis

### Detailed Candidate Sequences

#### GWHPCBHR005103 (OcMT-PF01)
```
MSCCGGNCGCGSGCKCGSGCGGCKMYPEMAEEVTTTQTVIMGVAPSKGHAEGLEAGAAAG
AGAENGCKCGDNCTCNPCTCGK
```
- **Length**: 82 aa
- **Theoretical pI**: 5.13
- **MW**: 7838.90 Da
- **Cys content**: 14 (17.1%)
- **Instability Index**: 38.87 (stable)
- **GRAVY**: -0.070

#### GWHPCBHR005104 (OcMT-PF02)
```
MSCCGGNCGCGSGCKCGSGCGGCKMYPEMAEEVTTTQTVIMGVAPSKGYVHQSFLRLHALYL
```
- **Length**: 62 aa
- **Theoretical pI**: 7.53
- **MW**: 6414.48 Da
- **Cys content**: 8 (12.9%)
- **Instability Index**: 56.53 (unstable)
- **GRAVY**: 0.168

#### GWHPCBHR063750 (OcMT-PF05)
```
MSCSCGSSCSCGSNCSCGKKYPDLEEKSSSAQATVVLGVAPEKKAQFEAAAESGETAHGC
SCGSNCKCNPCNC
```
- **Length**: 73 aa
- **Theoretical pI**: 5.66
- **MW**: 7323.16 Da
- **Cys content**: 12 (16.4%)
- **Instability Index**: 54.95 (unstable)
- **GRAVY**: -0.322

#### GWHPCBHR065057 (OcMT-PF06)
```
MSCGGSCNCGSSCGCGCGKMYPDLAEKNTTTTTISVTMVLGVAPEKGFQVAADSGEAAHG
CSCGSSCNCNPCNC
```
- **Length**: 74 aa
- **Theoretical pI**: 4.90
- **MW**: 7269.18 Da
- **Cys content**: 12 (16.2%)
- **Instability Index**: 47.61 (unstable)
- **GRAVY**: 0.039

#### GWHPCBHR065058 (OcMT-PF07)
```
MSCGGSCNCGSCDCGGGCGKMYPDLAEKITTTTTTATTVLGVAPEKGHFEAVGKVGEYGE
AAHGCSCGSSCKCNPCNC
```
- **Length**: 78 aa
- **Theoretical pI**: 5.48
- **MW**: 7708.68 Da
- **Cys content**: 12 (15.4%)
- **Instability Index**: 42.15 (unstable)
- **GRAVY**: -0.103

#### GWHPCBHR066751 (OcMT-PF09)
```
MSCGGSCNCGSSCKCGSGCGYDFSVKMYPDLADKNTTTTSATMVIGVAPEKGSGEAGFEV
AAGSGEAAEGCGCGSSCKCNPCNC
```
- **Length**: 84 aa
- **Theoretical pI**: 4.55
- **MW**: 8160.09 Da
- **Cys content**: 12 (14.3%)
- **Instability Index**: 41.13 (unstable)
- **GRAVY**: -0.076

#### GWHPCBHR066752 (OcMT-PF10)
```
MSCGGSCNCGSCGCGGGCGKMYPDLAEKITATTTAATTVLGVAPEKGHFEGIEKATESGE
AAHGCSCGSSCKCNPCNC
```
- **Length**: 78 aa
- **Theoretical pI**: 5.50
- **MW**: 7602.56 Da
- **Cys content**: 12 (15.4%)
- **Instability Index**: 55.58 (unstable)
- **GRAVY**: -0.091

---

## 10. Phylogenetic and Sequence Analysis

### Multiple Sequence Alignment
- **Tool**: MAFFT (EBI)
- **Job ID**: mafft-I20260811-220507-0365-89790442-p1m

### Phylogenetic Tree
*[Insert phylogenetic tree image here]*

### Identity Matrix Analysis
*[Insert identity matrix visualization here]*

**Key Finding**: GWHPCBHR005104 (OcMT-PF02) shows the lowest sequence identity among candidates, suggesting it may represent a more divergent metallothionein variant.

---

## 11. 3D Structure Prediction

### GWHPCBHR005103 (OcMT-PF01)
*[Insert 3D structure images here]*

Multiple structural models were generated to assess:
- Cysteine residue positioning
- Metal-binding site architecture
- Overall fold conservation with known metallothioneins

---

## 12. Key Concepts and Definitions

### Accession
A protein accession ID is a stable, unique alphanumeric identifier assigned to a specific protein sequence in biological databases like UniProt or NCBI. These IDs are used to unambiguously cite protein sequences in scientific literature and track them over time across databases.

### Null Model
The "null model" calculates the probability that the target sequence is not homologous to the query profile. It is a one-state HMM configured to generate "random" sequences of the same mean length L as the target sequence, with each residue drawn from a background frequency distribution (a standard i.i.d. model: residues are treated as independent and identically distributed). This background frequency is based on the mean residue frequencies in Swiss-Prot 50.8 (October 2006).

---

## 13. Resources and References

### Databases
- [Pfam PF01439 Logo](https://www.ebi.ac.uk/interpro/entry/pfam/PF01439/logo/)
- [NCBI Protein Database](https://www.ncbi.nlm.nih.gov/protein)
- [UniProt](http://www.uniprot.org/)

### Tools
- [HMMER User Guide](http://eddylab.org/software/hmmer3/3.1b1/Userguide.pdf)
- [HMMER Web Documentation](https://hmmer-web-docs.readthedocs.io/en/latest/searches.html#advanced-search-options)
- [Expasy ProtParam](https://web.expasy.org/protparam/)
- [NCBI BLAST](https://blast.ncbi.nlm.nih.gov/Blast.cgi)
- [MAFFT](https://www.ebi.ac.uk/jdispatcher/msa/mafft)

### Documentation
- [HMMER Result Interpretation](https://hmmer-web-docs.readthedocs.io/en/latest/result.html)

---

## Appendix: GitHub Setup

### Initial Setup
1. Create repository on GitHub
2. Name it (e.g., `01_homolog_oc`)
3. Copy HTTPS URL from GitHub

### Configure Local Repository
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/yourusername/reponame.git
git push -u origin main
```

### Personal Access Token Generation
1. Go to https://github.com/settings/tokens
2. Click "Generate new token (classic)"
3. Name: git-cli
4. Check scopes: `repo` (required), `workflow` (optional)
5. Set expiration (90 days)
6. Click "Generate token" and **copy immediately**

### Push Changes
```bash
git add .
git commit -m "Description of changes"
git push
```

### .gitignore Example
```
__pycache__/
*.pyc
*.log
*.tmp
.DS_Store
venv/
env/
results/
output/
```