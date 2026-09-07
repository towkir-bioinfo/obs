---
type: note
date: 2026-08-20
tags:
  - dna-extraction
  - reagents
legacy-status: reference
---
>[!info] Defination:
> **3 M sodium acetate, pH 5.2** — the salt added at 1/10 volume before alcohol precipitation of DNA. It supplies the counter-ions that let DNA aggregate and drop out of solution.

## Why it is used

DNA's phosphate backbone is **negatively charged**, so the strands repel each other and stay dissolved. Alcohol alone strips the water shell but does not neutralise that charge.

Na⁺ ions shield the phosphate backbone → repulsion collapses → DNA aggregates and precipitates. **Without salt, the DNA largely stays in solution and yield craters.**

## Why these specific numbers

| Parameter | Value | Reason |
|---|---|---|
| Concentration | 3 M | Gives ~0.3 M final at 1/10 volume — the empirical optimum |
| Volume | 1/10 of sample | 500 µL sample → 50 µL NaOAc |
| pH | 5.2 | Slightly acidic keeps DNA protonated/neutral and stable; avoids the alkaline range that promotes hydrolysis |
| Isopropanol | ~0.7 vol, ice-cold | Precipitates DNA at lower volume than ethanol; cold improves recovery |

## Practical points

- Precipitate **cold** (−20 °C) to maximise yield — hence "store it in −20 °C freezer".
- Isopropanol co-precipitates salt more than ethanol does, so a **70% ethanol wash** afterwards is important to remove residual NaOAc before resuspension.
- Alternative: ammonium acetate is preferred when carryover salt would inhibit downstream enzymes.

## Related

- [[02_knocout_os_ctab_dna_extraction_protocol]]
- [[CTAB]] · [[PCI]] · [[β-mercaptoethanol]]

```dataview
TABLE file.cday AS "Created Date"
FROM [[#]] AND -"_templates"
WHERE status = "active" OR "reference"
SORT file.cday DESC
```
