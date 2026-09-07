---
type: note
date: 2026-08-20
tags:
  - dna-extraction
  - reagents
legacy-status: reference
---
>[!info] Defination:
> **2-mercaptoethanol (β-ME)** — a reducing agent added fresh to [[CTAB]] buffer immediately before use. It breaks disulfide bonds and, in plant work, suppresses the phenolic browning that degrades and contaminates DNA.

## Why it is needed

Two jobs, both critical in plant tissue:

1. **Reduces disulfide bonds** → denatures and inactivates proteins, including **DNases** that would otherwise chew up the genomic DNA the moment the cell is lysed.
2. **Blocks phenolic oxidation.** Plant cells are loaded with polyphenols. When tissue is crushed, **polyphenol oxidase** converts them to quinones, which cross-link irreversibly to DNA and protein — the sample turns brown, and the DNA becomes degraded, brown-tinged, and PCR-inhibiting. β-ME keeps these compounds reduced so the reaction never runs.

This is why it matters more in plant extraction than in animal-tissue protocols.

## Practical points

- **Add fresh, immediately before use** — it oxidises in air, so buffer stored with β-ME already in it loses potency.
- Typical **0.2–2%** (the bench record used 40 µL into 20 mL ≈ 0.2%).
- Volatile and foul-smelling; **carcinogenic and acutely toxic**.

> [!warning] Safety
> Mix **outside** or in a fume hood. Gloves and mask required. This is why the protocol says "mix out side the beta is cancenognic".

## Related

- [[02_knocout_os_ctab_dna_extraction_protocol]]
- [[CTAB]] · [[PCI]] · [[Sodium acetate]]

```dataview
TABLE file.cday AS "Created Date"
FROM [[#]] AND -"_templates"
WHERE status = "active" OR "reference"
SORT file.cday DESC
```
