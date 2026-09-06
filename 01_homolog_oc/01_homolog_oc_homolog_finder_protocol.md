---
type: protocol
status: active
project: "[[01_homolog_oc_moc]]"
experiment: "[[P001-E001_MT-genome-wide-identification]]"
date: 2026-08-11
tags:
  - metallothioneins
  - oryza-coarctata
  - homology
  - gene-family
  - pipelines
---

# Homolog Finder of *O. coarctata*

Working record of the genome-wide metallothionein homolog search in the
*Oryza coarctata* proteome, using the Pfam PF01439 (Metallothio_2) profile
with HMMER, followed by filtering, candidate extraction, BLAST verification,
ProtParam characterisation and MAFFT alignment.

> [!info] Analysis directory
> `/home/cblast/towkir/projects/01_homolog_oc/`
> Proteome: `proteinocGWHCBHR00000000.faa` · Profile: `PF01439.hmm`

> [!warning] Sections needing your input
> Result, Interpretation and Next iteration are not written here. The
> candidate table in section 7 lists 11 IDs; the ProtParam table in section 9
> lists 8. Confirm which set is current before citing either.

## Contents

1. [[#1. Pfam profile and HMMER search]]
2. [[#2. Output tables]]
3. [[#3. Result filtering]]
4. [[#4. Bias percentage]]
5. [[#5. Filter criteria]]
6. [[#6. Candidate extraction workflow]]
7. [[#7. Candidate proteins]]
8. [[#8. BLAST verification]]
9. [[#9. Physicochemical characterisation (ProtParam)]]
10. [[#10. Alignment and phylogeny]]
11. [[#11. Per-candidate ProtParam output]]

---

## 1. Pfam profile and HMMER search

[https://www.ebi.ac.uk/interpro/entry/pfam/PF01439/logo/](https://www.ebi.ac.uk/interpro/entry/pfam/PF01439/logo/) link

 Pfam hmm download

|   |   |
|---|---|
|Situation|Tool|
|One/few HMM profiles → search a proteome|hmmsearch|
|Protein(s) → search against many Pfam HMMs|hmmscan|

PF01439.hmm

```text
      ↓
   hmmsearch
      ↓
```

O. coarctata proteome

```text
>Code
```

```bash
cd /home/cblast/towkir/projects/01_homolog_oc/data/raw/
hmmsearch --cpu 32 \
  --tblout "/home/cblast/towkir/projects/01_homolog_oc/result/table/PF01439_hits.tbl" \
  "/home/cblast/towkir/projects/01_homolog_oc/data/raw/PF01439.hmm" \
  "/home/cblast/towkir/projects/01_homolog_oc/data/raw/proteinocGWHCBHR00000000.faa" \
  > "/home/cblast/towkir/projects/01_homolog_oc/result/table/PF01439_full.txt"
```

01_homolog_oc/

```text
├── data/
│   └── raw/
│       ├── PF01439.hmm
│       └── proteinocGWHCBHR00000000.faa
└── result/
    └── table/
        ├── PF01439_hits.tbl
        └── PF01439_full.txt
```

|   |   |   |
|---|---|---|
|File|Main purpose|What it represents|
|--tblout hits.tbl|Protein/hit screening|How significantly each target protein matches your HMM|
|--domtblout domains.tbl|Domain analysis|Individual HMM domains detected within each protein|

## 2. Output tables

**Domain table**

```bash
hmmsearch \
  --domtblout domtblout.txt \
  PF01439.hmm \
  proteinocGWHCBHR00000000.faa \
  > /dev/null    #Hides the massive, human-readable default terminal output since results are already saved to the table.
```

## 3. Result filtering

### Result filter

### Table format

1. Target name → done (few has  different names)

2. [Accession](https://docs.google.com/document/d/16r2Kkqzt8NP_wonLNdmlz8ogUXnpVG0d3nqumjre-_s/edit?tab=t.j6ncwyefzcm#heading=h.sovy5sj7c5zj) → none has this (because it is a raw proteom data→ combine with gff we can get the acc)

3. query name (Metallothio_2)--> this is the pfam domain

4. Accession (of query) (PF01439.24 ) expected

5. E-value (full sequence) (we have one query it is ok) [for multiple query](http://eddylab.org/software/hmmer3/3.1b1/Userguide.pdf)cheeac

Check what e value remain what hits

**Single value**

```bash
awk '!/^#/ && $5 <= 1e-3' PF01439_hits.tbl | wc -l
```

**For multiple value**

```bash
for e in 0.05 1e-3 1e-5 1e-10; do
    echo "E-value <= $e: $(awk -v e="$e" '!/^#/ && $5 <= e' PF01439_hits.tbl | wc -l)"
done
```

E-value <= 0.05: 20

E-value <= 1e-3: 16

E-value <= 1e-5: 14

E-value <= 1e-10: 13

Go with the maximum for now 5% it is

6. score (full sequence) →23 (according to TC and GC)

My hmm curators  has some pre cutoffs

TC → trusted score (lowest bitscore that is a true homolog while creating the hmm profile)

GC→Gatthering score (for full family)

NC → Noise score (below this are noise)

**Code**

```bash
grep -E '^GA |^TC |^NC ' PF01439.hmm
```

**Output**

GA    23 23;

TC    23 23;

NC    22.9 22.9;

**Code**

```bash
awk '$0 !~ /^#/ {
```

    if ($6 >= 22) n22++;

    if ($6 >= 23) n23++;

    if ($6 >= 21) n21++;

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

**Output**

>=20: 17

>=30: 14

>=40: 13

>=50: 13

>=60: 13

>=70: 12

>=80: 6

7. Bias →too much bias (more than 35 only 3 less then 20)---> 40% bias is ok for this

[https://hmmer-web-docs.readthedocs.io/en/latest/searches.html#advanced-search-options](https://hmmer-web-docs.readthedocs.io/en/latest/searches.html#advanced-search-options)

Very useful …bais off can be tried

## 4. Bias percentage

|   |   |   |   |
|---|---|---|---|
|Target Sequence ID|Score|Bias|Bias%|
|GWHPCBHR005103|105.0|37.6|35.81%|
|GWHPCBHR066752|90.3|27.8|30.79%|
|GWHPCBHR066751|89.9|28.9|32.15%|
|GWHPCBHR065072|89.8|28.3|31.51%|
|GWHPCBHR065058|88.0|26.8|30.45%|
|GWHPCBHR005104|80.5|14.1|17.52%|
|GWHPCBHR063750|79.5|27.6|34.72%|
|GWHPCBHR019593|78.7|25.9|32.91%|
|GWHPCBHR019591|77.8|25.9|33.29%|
|GWHPCBHR065057|77.4|27.1|35.01%|
|GWHPCBHR065056|75.1|31.1|41.41%|
|GWHPCBHR066753|70.6|5.8|8.22%|
|GWHPCBHR009782|66.0|49.1|74.39%|
|GWHPCBHR019592|34.2|32.4|94.74%|
|GWHPCBHR004781|24.2|38.6|159.50%|
|GWHPCBHR036715|22.7|9.1|40.09%|
|GWHPCBHR036714|21.0|9.4|44.76%|
|GWHPCBHR020560|17.3|1.3|7.51%|
|GWHPCBHR020561|17.3|1.3|7.51%|
|GWHPCBHR020562|17.3|1.3|7.51%|
|GWHPCBHR027668|15.7|1.2|7.64%|
|GWHPCBHR033849|15.1|22.6|149.67%|
|GWHPCBHR027667|14.9|0.2|1.34%|
|GWHPCBHR027665|14.1|0.3|2.13%|
|GWHPCBHR027666|14.1|0.3|2.13%|
|GWHPCBHR027664|13.7|0.3|2.19%|
|GWHPCBHR052046|11.9|3.4|28.57%|
|GWHPCBHR025293|11.4|0.1|0.88%|
|GWHPCBHR005525|9.8|27.0|275.51%|

The problem is metallothionein is highly cysteine  rich so null hypothesis makes score more and thus bias also not correct …

**Reason**

Metallothionein profiles can exhibit strong compositional bias because they are cysteine-rich. HMMER therefore applies a biased-composition correction (the null2 model) to account for scores that may arise from unusual residue composition rather than genuine profile–sequence similarity.

8. E-value (best 1 domain)--> this has to be good

**Reason**

If this E-value isn’t good, but the full sequence E-value is good, this is a potential red flag

9. score (best 1 domain) → not needed

10. bias (best 1 domain) → same

11. Exp (expected domain)--> ideally 2 but there is alot of 1

12. reg(doamin calculated) →same

New Filtered data

 4 criteria are use

1. =<40% pct

2. >=23 score(bit score)

3. =< 1e-3 E-value

4. Combine all

This is for hits table data

data/filtered/

```text
├── PF01439_evalue_1e-3.tbl
├── PF01439_score_over23.tbl
├── PF01439_bias_40pct_or_less.tbl
└── PF01439_combined.tbl
Path /home/cblast/towkir/projects/01_homolog_oc/data/filtered
```

## 5. Filter criteria

**Code & logics**

Bias percentage = (Bias / Bit Score) × 100

The output files were saved in:

```text
/home/cblast/towkir/projects/01_homolog_oc/data/filtered/
```

#### 1. E-value cutoff: ≤ 1 × 10⁻³

```bash
awk 'BEGIN{OFS="\t"} /^#/ {print; next} $5 <= 1e-3' PF01439_hits.tbl > /home/cblast/towkir/projects/01_homolog_oc/data/filtered/PF01439_evalue_1e-3.tbl
```

#### 2. Bit score cutoff: > 23

```bash
awk 'BEGIN{OFS="\t"} /^#/ {print; next} $6 > 23' PF01439_hits.tbl > /home/cblast/towkir/projects/01_homolog_oc/data/filtered/PF01439_score_over23.tbl
```

#### 3. Bias percentage cutoff: ≤ 40%

```bash
awk 'BEGIN{OFS="\t"} /^#/ {print; next} $6 != 0 && ($7/$6)*100 <= 40' PF01439_hits.tbl > /home/cblast/towkir/projects/01_homolog_oc/data/filtered/PF01439_bias_40pct_or_less.tbl
```

#### 4. Combined filtering

Hits satisfying all three criteria simultaneously were extracted using:

**E-value ≤ 1 × 10⁻³**

**Bit score > 23**

**Bias percentage ≤ 40%**

```bash
awk 'BEGIN{OFS="\t"} /^#/ {print; next} $5 <= 1e-3 && $6 > 23 && $6 != 0 && ($7/$6)*100 <= 40' PF01439_hits.tbl > /home/cblast/towkir/projects/01_homolog_oc/data/filtered/PF01439_combined.tbl
```

#### 5. Counting the number of retained hits

The number of hits in each filtered file was counted using:

```bash
for f in /home/cblast/towkir/projects/01_homolog_oc/data/filtered/PF01439*.tbl; do echo "$(basename "$f"): $(grep -vc '^#' "$f") hits"; done
```

Now workflow

## 6. Candidate extraction workflow

PF01439_filtered_hits.tbl

```text
          │
          │ sequence IDs
          ▼
```

      Proteome FASTA

```text
          │
          ▼
```

   Candidate proteins

```text
          │
          ├── length / sequence inspection
          ├── HMMER domain confirmation
          ├── cysteine-rich MT characteristics
          │
          ▼
```

       GFF annotation

```text
          │
          ▼
```

   gene ID ↔ protein ID ↔ CDS

```text
          │
          ▼
```

     genomic location

```text
          │
          ▼
```

        WGS

   (genomic sequence)

Steps

1. Make a txt file with all the name header

2. Match and make another file with protein extracted

**Code for txt**

```bash
awk '!/^#/ {print $1}' \
/home/cblast/towkir/projects/01_homolog_oc/data/filtered/PF01439_combined.tbl \
| sort -u \
> /home/cblast/towkir/projects/01_homolog_oc/data/filtered/PF01439_candidate_ids.txt
```

**Output**

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

**Check the heading of proteome**

```bash
grep '^>' /home/cblast/towkir/projects/01_homolog_oc/data/raw/.fasta | head
```

**Making the txt file**

```bash
awk '!/^#/ {print $1}' \
data/filtered/PF01439_combined.tbl \
| sort -u \
> data/filtered/PF01439_candidate_ids.txt
```

**Making the candidate files**

```bash
seqkit grep -f \
 data/filtered/PF01439_candidate_ids.txt \
 data/raw/proteinocGWHCBHR00000000.faa \
> data/filtered/PF01439_candidate_proteins.fasta     # ‘>’ is for piping into  a file
```

## 7. Candidate proteins

Candidate fasta table

|   |   |   |   |   |   |
|---|---|---|---|---|---|
|Presentation ID|Original protein ID|Gene|Transcript|Length|Notes|
|OcMT-PF01|GWHPCBHR005103|GWHGCBHR003334|Oco02G001920.1|69 aa|MT-like, cysteine-rich|
|OcMT-PF02|GWHPCBHR005104|GWHGCBHR003334|Oco02G001920.2|66 aa|Alternative transcript|
|OcMT-PF03|GWHPCBHR019591|GWHGCBHR012785|Oco05G010460.1|119 aa|Longer protein|
|OcMT-PF04|GWHPCBHR019593|GWHGCBHR012785|Oco05G010460.3|97 aa|Alternative transcript|
|OcMT-PF05|GWHPCBHR063750|GWHGCBHR042392|Oco22G011490.1|64 aa|Strong MT-like architecture|
|OcMT-PF06|GWHPCBHR065057|GWHGCBHR043283|Oco23G008740.1|65 aa|Strong MT-like architecture|
|OcMT-PF07|GWHPCBHR065058|GWHGCBHR043284|Oco23G008750.1|67 aa|Strong MT-like architecture|
|OcMT-PF08|GWHPCBHR065072|GWHGCBHR043298|Oco23G008890.1|66 aa|Strong MT-like architecture|
|OcMT-PF09|GWHPCBHR066751|GWHGCBHR044409|Oco24G008450.1|69 aa|Strong MT-like architecture|
|OcMT-PF10|GWHPCBHR066752|GWHGCBHR044410|Oco24G008460.1|67 aa|Strong MT-like architecture|
|OcMT-PF11|GWHPCBHR066753|GWHGCBHR044410|Oco24G008460.2|47 aa|Alternative transcript/shorter isoform|

## 8. BLAST verification

Do blast and ExpasyProtoparm

[Ocmt](https://www.ncbi.nlm.nih.gov/protein/WYV70274.1?report=fasta) [BLAST2](http://140.114.98.75/blast/wblast2.cgi?5)

[https://blast.ncbi.nlm.nih.gov/Blast.cgi#](https://blast.ncbi.nlm.nih.gov/Blast.cgi#)

![[P001-E001_fig01.png]]

![[P001-E001_fig02.png|700]]

|   |   |   |   |   |   |   |   |   |   |   |   |
|---|---|---|---|---|---|---|---|---|---|---|---|
## 9. Physicochemical characterisation (ProtParam)

|Protein|Status|Length (aa)|MW (kDa)|pI|Cys|Cys %|Neg|Pos|Instability Index|Aliphatic Index|GRAVY|
|WYV70274.1|OCMT reference|64|6.54|5.14|10|15.6|10|8|25.82|44.22|−0.470|
|GWHPCBHR005103|Candidate|82|7.84|5.13|14|17.1|7|5|38.87|31.10|−0.070|
|GWHPCBHR005104|Candidate|62|6.41|7.53|8|12.9|3|4|56.53|55.00|0.168|
|GWHPCBHR063750|Candidate|73|7.32|5.66|12|16.4|7|6|54.95|33.56|−0.322|
|GWHPCBHR065057|Candidate|74|7.27|4.90|12|16.2|5|3|47.61|39.59|0.039|
|GWHPCBHR065058|Candidate|78|7.71|5.48|12|15.4|7|5|42.15|37.56|−0.103|
|GWHPCBHR066751|Candidate|84|8.16|4.55|12|14.3|8|5|41.13|32.62|−0.076|
|GWHPCBHR066752|Candidate|78|7.60|5.50|12|15.4|7|5|55.58|||

The candidate proteins displayed physicochemical characteristics broadly comparable to the O. coarctata metallothionein reference, particularly in their short sequence lengths and high cysteine content. Among the candidates, GWHPCBHR005103 showed the closest theoretical pI to the reference protein and was predicted to be stable according to the ProtParam instability index. However, ProtParam characteristics alone were not used to establish metallothionein homology; sequence-level conservation, cysteine distribution, domain similarity, and phylogenetic relationships provide stronger evidence for candidate classification.

[https://www.ebi.ac.uk/jdispatcher/msa/mafft/summary?jobId=mafft-I20260811-220507-0365-89790442-p1m](https://www.ebi.ac.uk/jdispatcher/msa/mafft/summary?jobId=mafft-I20260811-220507-0365-89790442-p1m)

## 10. Alignment and phylogeny

Is used for the following phylogenetic tree

![[P001-E001_fig03.png]]

![[P001-E001_fig04.png]]

104 has the lowest identity!

![[P001-E001_fig05.png]]

![[P001-E001_fig06.png]]

![[P001-E001_fig07.png]]

![[P001-E001_fig08.png]]

```text
## 11. Per-candidate ProtParam output

### GWHPCBHR005103

>GWHPCBHR005103 mRNA=GWHTCBHR005103 Gene=GWHGCBHR003334 Position=GWHCBHR00000002: 1921412-1921517, 1921956-1922033, 1922538-1922602: - Frame=0 OriID=Oco02G001920.1 OriTrascriptID=Oco02G001920.1 transl_table=1 OriGeneID=Oco02G001920 OriSeqID=LG02
```

MSCCGGNCGCGSGCKCGSGCGGCKMYPEMAEEVTTTQTVIMGVAPSKGHAEGLEAGAAAG

AGAENGCKCGDNCTCNPCTCGK

**ProtParam output**

```text

       10         20         30         40         50         60

MSCCGGNCGC GSGCKCGSGC GGCKMYPEMA EEVTTTQTVI MGVAPSKGHA EGLEAGAAAG

       70         80

AGAENGCKCG DNCTCNPCTC GK

---

[[Documentation](https://web.expasy.org/protparam/protparam-doc.html) / [Reference](https://web.expasy.org/protparam/protpar-ref.html)]

---

Number of amino acids: 82

Theoretical pI: 5.13

Molecular weight: 7838.90

Amino acid composition: 

Ala (A)   9 11.0%

Arg (R)   0   0.0%

Asn (N)   4   4.9%

Asp (D)   1   1.2%

Cys (C)  14 17.1%

Gln (Q)   1   1.2%

Glu (E)   6   7.3%

Gly (G)  18 22.0%

His (H)   1   1.2%

Ile (I)   1   1.2%

Leu (L)   1   1.2%

Lys (K)   5   6.1%

Met (M)   4   4.9%

Phe (F)   0   0.0%

Pro (P)   3   3.7%

Ser (S)   4   4.9%

Thr (T)   6   7.3%

Trp (W)   0   0.0%

Tyr (Y)   1   1.2%

Val (V)   3   3.7%

Pyl (O)   0   0.0%

Sec (U)   0   0.0%

 (B)   0   0.0%

 (Z)   0   0.0%

 (X)   0   0.0%

Total number of negatively charged residues (Asp + Glu): 7

Total number of positively charged residues (Arg + Lys): 5

Atomic composition:

Carbon      C       303

Hydrogen    H       494

Nitrogen    N         94

Oxygen      O       113

Sulfur      S         18

Formula: C303H494N94O113S18

Total number of atoms: 1022

Extinction coefficients:

This protein does not contain any Trp residues. Experience shows that

this could result in more than 10% error in the computed extinction coefficient.

Extinction coefficients are in units of  M-1 cm-1, at 280 nm measured in water.

Ext. coefficient     2365

Abs 0.1% (=1 g/l)   0.302, assuming all pairs of Cys residues form cystines

Ext. coefficient     1490

Abs 0.1% (=1 g/l)   0.190, assuming all Cys residues are reduced

Estimated half-life:

The N-terminal of the sequence considered is M (Met).

The estimated half-life is: 30 hours (mammalian reticulocytes, in vitro).

                            >20 hours (yeast, in vivo).

                            >10 hours (Escherichia coli, in vivo).

Instability index:

The instability index (II) is computed to be 38.87

This classifies the protein as stable.

Aliphatic index: 31.10

Grand average of hydropathicity (GRAVY):-0.070
```

```text
### GWHPCBHR005104

>GWHPCBHR005104 mRNA=GWHTCBHR005104 Gene=GWHGCBHR003334 Position=GWHCBHR00000002: 1921910-1922033, 1922538-1922602: - Frame=0 OriID=Oco02G001920.2 OriTrascriptID=Oco02G001920.2 transl_table=1 OriGeneID=Oco02G001920 OriSeqID=LG02
```

MSCCGGNCGCGSGCKCGSGCGGCKMYPEMAEEVTTTQTVIMGVAPSKGYVHQSFLRLHAL

YL

**ProtParam output**

```text

       10         20         30         40         50         60

MSCCGGNCGC GSGCKCGSGC GGCKMYPEMA EEVTTTQTVI MGVAPSKGYV HQSFLRLHAL

YL

---

[[Documentation](https://web.expasy.org/protparam/protparam-doc.html) / [Reference](https://web.expasy.org/protparam/protpar-ref.html)]

---

Number of amino acids: 62

Theoretical pI: 7.53

Molecular weight: 6414.48

Amino acid composition: 

Ala (A)   3   4.8%

Arg (R)   1   1.6%

Asn (N)   1   1.6%

Asp (D)   0   0.0%

Cys (C)   8 12.9%

Gln (Q)   2   3.2%

Glu (E)   3   4.8%

Gly (G)  11 17.7%

His (H)   2   3.2%

Ile (I)   1   1.6%

Leu (L)   4   6.5%

Lys (K)   3   4.8%

Met (M)   4   6.5%

Phe (F)   1   1.6%

Pro (P)   2   3.2%

Ser (S)   5   8.1%

Thr (T)   4   6.5%

Trp (W)   0   0.0%

Tyr (Y)   3   4.8%

Val (V)   4   6.5%

Pyl (O)   0   0.0%

Sec (U)   0   0.0%

 (B)   0   0.0%

 (Z)   0   0.0%

 (X)   0   0.0%

Total number of negatively charged residues (Asp + Glu): 3

Total number of positively charged residues (Arg + Lys): 4

Atomic composition:

Carbon      C       267

Hydrogen    H       425

Nitrogen    N         75

Oxygen      O         84

Sulfur      S         12

Formula: C267H425N75O84S12

Total number of atoms: 863

Extinction coefficients:

This protein does not contain any Trp residues. Experience shows that

this could result in more than 10% error in the computed extinction coefficient.

Extinction coefficients are in units of  M-1 cm-1, at 280 nm measured in water.

Ext. coefficient     4970

Abs 0.1% (=1 g/l)   0.775, assuming all pairs of Cys residues form cystines

Ext. coefficient     4470

Abs 0.1% (=1 g/l)   0.697, assuming all Cys residues are reduced

Estimated half-life:

The N-terminal of the sequence considered is M (Met).

The estimated half-life is: 30 hours (mammalian reticulocytes, in vitro).

                            >20 hours (yeast, in vivo).

                            >10 hours (Escherichia coli, in vivo).

Instability index:

The instability index (II) is computed to be 56.53

This classifies the protein as unstable.

Aliphatic index: 55.00

Grand average of hydropathicity (GRAVY):0.168
```

```text
### GWHPCBHR063750

>GWHPCBHR063750 mRNA=GWHTCBHR063750 Gene=GWHGCBHR042392 Position=GWHCBHR00000022: 14978875-14978927, 14979096-14979264: + Frame=0 OriID=Oco22G011490.1 OriTrascriptID=Oco22G011490.1 transl_table=1 OriGeneID=Oco22G011490 OriSeqID=LG22
```

MSCSCGSSCSCGSNCSCGKKYPDLEEKSSSAQATVVLGVAPEKKAQFEAAAESGETAHGC

SCGSNCKCNPCNC

**ProtParam output**

```text

       10         20         30         40         50         60

MSCSCGSSCS CGSNCSCGKK YPDLEEKSSS AQATVVLGVA PEKKAQFEAA AESGETAHGC

       70

SCGSNCKCNP CNC

---

[[Documentation](https://web.expasy.org/protparam/protparam-doc.html) / [Reference](https://web.expasy.org/protparam/protpar-ref.html)]

---

Number of amino acids: 73

Theoretical pI: 5.66

Molecular weight: 7323.16

Amino acid composition: 

Ala (A)   8 11.0%

Arg (R)   0   0.0%

Asn (N)   4   5.5%

Asp (D)   1   1.4%

Cys (C)  12 16.4%

Gln (Q)   2   2.7%

Glu (E)   6   8.2%

Gly (G)   7   9.6%

His (H)   1   1.4%

Ile (I)   0   0.0%

Leu (L)   2   2.7%

Lys (K)   6   8.2%

Met (M)   1   1.4%

Phe (F)   1   1.4%

Pro (P)   3   4.1%

Ser (S)  13 17.8%

Thr (T)   2   2.7%

Trp (W)   0   0.0%

Tyr (Y)   1   1.4%

Val (V)   3   4.1%

Pyl (O)   0   0.0%

Sec (U)   0   0.0%

 (B)   0   0.0%

 (Z)   0   0.0%

 (X)   0   0.0%

Total number of negatively charged residues (Asp + Glu): 7

Total number of positively charged residues (Arg + Lys): 6

Atomic composition:

Carbon      C       288

Hydrogen    H       465

Nitrogen    N         87

Oxygen      O       110

Sulfur      S         13

Formula: C288H465N87O110S13

Total number of atoms: 963

Extinction coefficients:

This protein does not contain any Trp residues. Experience shows that

this could result in more than 10% error in the computed extinction coefficient.

Extinction coefficients are in units of  M-1 cm-1, at 280 nm measured in water.

Ext. coefficient     2240

Abs 0.1% (=1 g/l)   0.306, assuming all pairs of Cys residues form cystines

Ext. coefficient     1490

Abs 0.1% (=1 g/l)   0.203, assuming all Cys residues are reduced

Estimated half-life:

The N-terminal of the sequence considered is M (Met).

The estimated half-life is: 30 hours (mammalian reticulocytes, in vitro).

                            >20 hours (yeast, in vivo).

                            >10 hours (Escherichia coli, in vivo).

Instability index:

The instability index (II) is computed to be 54.95

This classifies the protein as unstable.

Aliphatic index: 33.56

Grand average of hydropathicity (GRAVY):-0.322
```

```text
### GWHPCBHR065057

>GWHPCBHR065057 mRNA=GWHTCBHR065057 Gene=GWHGCBHR043283 Position=GWHCBHR00000023: 14376823-14376907, 14377058-14377144, 14377366-14377418: - Frame=0 OriID=Oco23G008740.1 OriTrascriptID=Oco23G008740.1 transl_table=1 OriGeneID=Oco23G008740 OriSeqID=LG23
```

MSCGGSCNCGSSCGCGCGKMYPDLAEKNTTTTTISVTMVLGVAPEKGFQVAADSGEAAHG

CSCGSSCNCNPCNC

**ProtParam output**

```text

       10         20         30         40         50         60

MSCGGSCNCG SSCGCGCGKM YPDLAEKNTT TTTISVTMVL GVAPEKGFQV AADSGEAAHG

       70

CSCGSSCNCN PCNC

---

[[Documentation](https://web.expasy.org/protparam/protparam-doc.html) / [Reference](https://web.expasy.org/protparam/protpar-ref.html)]

---

Number of amino acids: 74

Theoretical pI: 4.90

Molecular weight: 7269.18

Amino acid composition: 

Ala (A)   6   8.1%

Arg (R)   0   0.0%

Asn (N)   5   6.8%

Asp (D)   2   2.7%

Cys (C)  12 16.2%

Gln (Q)   1   1.4%

Glu (E)   3   4.1%

Gly (G)  11 14.9%

His (H)   1   1.4%

Ile (I)   1   1.4%

Leu (L)   2   2.7%

Lys (K)   3   4.1%

Met (M)   3   4.1%

Phe (F)   1   1.4%

Pro (P)   3   4.1%

Ser (S)   9 12.2%

Thr (T)   6   8.1%

Trp (W)   0   0.0%

Tyr (Y)   1   1.4%

Val (V)   4   5.4%

Pyl (O)   0   0.0%

Sec (U)   0   0.0%

 (B)   0   0.0%

 (Z)   0   0.0%

 (X)   0   0.0%

Total number of negatively charged residues (Asp + Glu): 5

Total number of positively charged residues (Arg + Lys): 3

Atomic composition:

Carbon      C       285

Hydrogen    H       459

Nitrogen    N         85

Oxygen      O       107

Sulfur      S         15

Formula: C285H459N85O107S15

Total number of atoms: 951

Extinction coefficients:

This protein does not contain any Trp residues. Experience shows that

this could result in more than 10% error in the computed extinction coefficient.

Extinction coefficients are in units of  M-1 cm-1, at 280 nm measured in water.

Ext. coefficient     2240

Abs 0.1% (=1 g/l)   0.308, assuming all pairs of Cys residues form cystines

Ext. coefficient     1490

Abs 0.1% (=1 g/l)   0.205, assuming all Cys residues are reduced

Estimated half-life:

The N-terminal of the sequence considered is M (Met).

The estimated half-life is: 30 hours (mammalian reticulocytes, in vitro).

                            >20 hours (yeast, in vivo).

                            >10 hours (Escherichia coli, in vivo).

Instability index:

The instability index (II) is computed to be 47.61

This classifies the protein as unstable.

Aliphatic index: 39.59

Grand average of hydropathicity (GRAVY):0.039
```

```text
### GWHPCBHR065058

>GWHPCBHR065058 mRNA=GWHTCBHR065058 Gene=GWHGCBHR043284 Position=GWHCBHR00000023: 14385880-14385976, 14386085-14386168, 14386432-14386487: - Frame=0 OriID=Oco23G008750.1 OriTrascriptID=Oco23G008750.1 transl_table=1 OriGeneID=Oco23G008750 OriSeqID=LG23
```

MSCGGSCNCGSCDCGGGCGKMYPDLAEKITTTTTTATTVLGVAPEKGHFEAVGKVGEYGE

AAHGCSCGSSCKCNPCNC

**ProtParam output**

```text

       10         20         30         40         50         60

MSCGGSCNCG SCDCGGGCGK MYPDLAEKIT TTTTTATTVL GVAPEKGHFE AVGKVGEYGE

       70

AAHGCSCGSS CKCNPCNC

---

[[Documentation](https://web.expasy.org/protparam/protparam-doc.html) / [Reference](https://web.expasy.org/protparam/protpar-ref.html)]

---

Number of amino acids: 78

Theoretical pI: 5.48

Molecular weight: 7708.68

Amino acid composition: 

Ala (A)   6   7.7%

Arg (R)   0   0.0%

Asn (N)   3   3.8%

Asp (D)   2   2.6%

Cys (C)  12 15.4%

Gln (Q)   0   0.0%

Glu (E)   5   6.4%

Gly (G)  14 17.9%

His (H)   2   2.6%

Ile (I)   1   1.3%

Leu (L)   2   2.6%

Lys (K)   5   6.4%

Met (M)   2   2.6%

Phe (F)   1   1.3%

Pro (P)   3   3.8%

Ser (S)   6   7.7%

Thr (T)   8 10.3%

Trp (W)   0   0.0%

Tyr (Y)   2   2.6%

Val (V)   4   5.1%

Pyl (O)   0   0.0%

Sec (U)   0   0.0%

 (B)   0   0.0%

 (Z)   0   0.0%

 (X)   0   0.0%

Total number of negatively charged residues (Asp + Glu): 7

Total number of positively charged residues (Arg + Lys): 5

Atomic composition:

Carbon      C       309

Hydrogen    H       492

Nitrogen    N         90

Oxygen      O       112

Sulfur      S         14

Formula: C309H492N90O112S14

Total number of atoms: 1017

Extinction coefficients:

This protein does not contain any Trp residues. Experience shows that

this could result in more than 10% error in the computed extinction coefficient.

Extinction coefficients are in units of  M-1 cm-1, at 280 nm measured in water.

Ext. coefficient     3730

Abs 0.1% (=1 g/l)   0.484, assuming all pairs of Cys residues form cystines

Ext. coefficient     2980

Abs 0.1% (=1 g/l)   0.387, assuming all Cys residues are reduced

Estimated half-life:

The N-terminal of the sequence considered is M (Met).

The estimated half-life is: 30 hours (mammalian reticulocytes, in vitro).

                            >20 hours (yeast, in vivo).

                            >10 hours (Escherichia coli, in vivo).

Instability index:

The instability index (II) is computed to be 42.15

This classifies the protein as unstable.

Aliphatic index: 37.56

Grand average of hydropathicity (GRAVY):-0.103

MSCGGSCNCGSCGCGGGCGKMYPDLAEKITTTTTATTVLGVAPEKGQFERVGKAAETGEG

AHGCSCGSSCKCNPCNC
```

**ProtParam output**

```text

       10         20         30         40         50         60

MSCGGSCNCG SCGCGGGCGK MYPDLAEKIT TTTTATTVLG VAPEKGQFER VGKAAETGEG

       70

AHGCSCGSSC KCNPCNC

---

[[Documentation](https://web.expasy.org/protparam/protparam-doc.html) / [Reference](https://web.expasy.org/protparam/protpar-ref.html)]

---

Number of amino acids: 77

Theoretical pI: 6.50

Molecular weight: 7535.51

Amino acid composition: 

Ala (A)   6   7.8%

Arg (R)   1   1.3%

Asn (N)   3   3.9%

Asp (D)   1   1.3%

Cys (C)  12 15.6%

Gln (Q)   1   1.3%

Glu (E)   5   6.5%

Gly (G)  15 19.5%

His (H)   1   1.3%

Ile (I)   1   1.3%

Leu (L)   2   2.6%

Lys (K)   5   6.5%

Met (M)   2   2.6%

Phe (F)   1   1.3%

Pro (P)   3   3.9%

Ser (S)   6   7.8%

Thr (T)   8 10.4%

Trp (W)   0   0.0%

Tyr (Y)   1   1.3%

Val (V)   3   3.9%

Pyl (O)   0   0.0%

Sec (U)   0   0.0%

 (B)   0   0.0%

 (Z)   0   0.0%

 (X)   0   0.0%

Total number of negatively charged residues (Asp + Glu): 6

Total number of positively charged residues (Arg + Lys): 6

Atomic composition:

Carbon      C       298

Hydrogen    H       485

Nitrogen    N         91

Oxygen      O       109

Sulfur      S         14

Formula: C298H485N91O109S14

Total number of atoms: 997

Extinction coefficients:

This protein does not contain any Trp residues. Experience shows that

this could result in more than 10% error in the computed extinction coefficient.

Extinction coefficients are in units of  M-1 cm-1, at 280 nm measured in water.

Ext. coefficient     2240

Abs 0.1% (=1 g/l)   0.297, assuming all pairs of Cys residues form cystines

Ext. coefficient     1490

Abs 0.1% (=1 g/l)   0.198, assuming all Cys residues are reduced

Estimated half-life:

The N-terminal of the sequence considered is M (Met).

The estimated half-life is: 30 hours (mammalian reticulocytes, in vitro).

                            >20 hours (yeast, in vivo).

                            >10 hours (Escherichia coli, in vivo).

Instability index:

The instability index (II) is computed to be 42.52

This classifies the protein as unstable.

Aliphatic index: 34.29

Grand average of hydropathicity (GRAVY):-0.164
```

```text
### GWHPCBHR066751

>GWHPCBHR066751 mRNA=GWHTCBHR066751 Gene=GWHGCBHR044409 Position=GWHCBHR00000024: 13405698-13405771, 13412607-13412687, 13412812-13412911: + Frame=0 OriID=Oco24G008450.1 OriTrascriptID=Oco24G008450.1 transl_table=1 OriGeneID=Oco24G008450 OriSeqID=LG24
```

MSCGGSCNCGSSCKCGSGCGYDFSVKMYPDLADKNTTTTSATMVIGVAPEKGSGEAGFEV

AAGSGEAAEGCGCGSSCKCNPCNC

**ProtParam output**

```text

       10         20         30         40         50         60

MSCGGSCNCG SSCKCGSGCG YDFSVKMYPD LADKNTTTTS ATMVIGVAPE KGSGEAGFEV

       70         80

AAGSGEAAEG CGCGSSCKCN PCNC

---

[[Documentation](https://web.expasy.org/protparam/protparam-doc.html) / [Reference](https://web.expasy.org/protparam/protpar-ref.html)]

---

Number of amino acids: 84

Theoretical pI: 4.55

Molecular weight: 8160.09

Amino acid composition: 

Ala (A)   8   9.5%

Arg (R)   0   0.0%

Asn (N)   4   4.8%

Asp (D)   3   3.6%

Cys (C)  12 14.3%

Gln (Q)   0   0.0%

Glu (E)   5   6.0%

Gly (G)  15 17.9%

His (H)   0   0.0%

Ile (I)   1   1.2%

Leu (L)   1   1.2%

Lys (K)   5   6.0%

Met (M)   3   3.6%

Phe (F)   2   2.4%

Pro (P)   3   3.6%

Ser (S)  11 13.1%

Thr (T)   5   6.0%

Trp (W)   0   0.0%

Tyr (Y)   2   2.4%

Val (V)   4   4.8%

Pyl (O)   0   0.0%

Sec (U)   0   0.0%

 (B)   0   0.0%

 (Z)   0   0.0%

 (X)   0   0.0%

Total number of negatively charged residues (Asp + Glu): 8

Total number of positively charged residues (Arg + Lys): 5

Atomic composition:

Carbon      C       324

Hydrogen    H       513

Nitrogen    N         93

Oxygen      O       123

Sulfur      S         15

Formula: C324H513N93O123S15

Total number of atoms: 1068

Extinction coefficients:

This protein does not contain any Trp residues. Experience shows that

this could result in more than 10% error in the computed extinction coefficient.

Extinction coefficients are in units of  M-1 cm-1, at 280 nm measured in water.

Ext. coefficient     3730

Abs 0.1% (=1 g/l)   0.457, assuming all pairs of Cys residues form cystines

Ext. coefficient     2980

Abs 0.1% (=1 g/l)   0.365, assuming all Cys residues are reduced

Estimated half-life:

The N-terminal of the sequence considered is M (Met).

The estimated half-life is: 30 hours (mammalian reticulocytes, in vitro).

                            >20 hours (yeast, in vivo).

                            >10 hours (Escherichia coli, in vivo).

Instability index:

The instability index (II) is computed to be 41.13

This classifies the protein as unstable.

Aliphatic index: 32.62

Grand average of hydropathicity (GRAVY):-0.076
```

```text
### GWHPCBHR066752

>GWHPCBHR066752 mRNA=GWHTCBHR066752 Gene=GWHGCBHR044410 Position=GWHCBHR00000024: 13415443-13415498, 13415776-13415859, 13421691-13421787: + Frame=0 OriID=Oco24G008460.1 OriTrascriptID=Oco24G008460.1 transl_table=1 OriGeneID=Oco24G008460 OriSeqID=LG24
```

MSCGGSCNCGSCGCGGGCGKMYPDLAEKITATTTAATTVLGVAPEKGHFEGIEKATESGE

AAHGCSCGSSCKCNPCNC

**ProtParam output**

```text

       10         20         30         40         50         60

MSCGGSCNCG SCGCGGGCGK MYPDLAEKIT ATTTAATTVL GVAPEKGHFE GIEKATESGE

       70

AAHGCSCGSS CKCNPCNC

---

[[Documentation](https://web.expasy.org/protparam/protparam-doc.html) / [Reference](https://web.expasy.org/protparam/protpar-ref.html)]

---

Number of amino acids: 78

Theoretical pI: 5.50

Molecular weight: 7602.56

Amino acid composition: 

Ala (A)   8 10.3%

Arg (R)   0   0.0%

Asn (N)   3   3.8%

Asp (D)   1   1.3%

Cys (C)  12 15.4%

Gln (Q)   0   0.0%

Glu (E)   6   7.7%

Gly (G)  14 17.9%

His (H)   2   2.6%

Ile (I)   2   2.6%

Leu (L)   2   2.6%

Lys (K)   5   6.4%

Met (M)   2   2.6%

Phe (F)   1   1.3%

Pro (P)   3   3.8%

Ser (S)   7   9.0%

Thr (T)   7   9.0%

Trp (W)   0   0.0%

Tyr (Y)   1   1.3%

Val (V)   2   2.6%

Pyl (O)   0   0.0%

Sec (U)   0   0.0%

 (B)   0   0.0%

 (Z)   0   0.0%

 (X)   0   0.0%

Total number of negatively charged residues (Asp + Glu): 7

Total number of positively charged residues (Arg + Lys): 5

Atomic composition:

Carbon      C       302

Hydrogen    H       486

Nitrogen    N         90

Oxygen      O       111

Sulfur      S         14

Formula: C302H486N90O111S14

Total number of atoms: 1003

Extinction coefficients:

This protein does not contain any Trp residues. Experience shows that

this could result in more than 10% error in the computed extinction coefficient.

Extinction coefficients are in units of  M-1 cm-1, at 280 nm measured in water.

Ext. coefficient     2240

Abs 0.1% (=1 g/l)   0.295, assuming all pairs of Cys residues form cystines

Ext. coefficient     1490

Abs 0.1% (=1 g/l)   0.196, assuming all Cys residues are reduced

Estimated half-life:

The N-terminal of the sequence considered is M (Met).

The estimated half-life is: 30 hours (mammalian reticulocytes, in vitro).

                            >20 hours (yeast, in vivo).

                            >10 hours (Escherichia coli, in vivo).

Instability index:

The instability index (II) is computed to be 55.58

This classifies the protein as unstable.

Aliphatic index: 37.69

Grand average of hydropathicity (GRAVY):-0.091
```
