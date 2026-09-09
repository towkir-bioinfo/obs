---
type: note
date: 2026-08-20
tags:
  - dna-extraction
  - reagents
legacy-status: reference
---
>[!info] Defination:
> **Cetyltrimethylammonium bromide** — a cationic detergent used as the lysis buffer base for plant genomic DNA extraction. It solubilises membranes and, critically, forms an insoluble complex with polysaccharides so they can be separated away from nucleic acids.

## Why it is used (not just any detergent)

Plant tissue is full of **polysaccharides** (cell wall, mucilage) that co-purify with DNA and then inhibit downstream enzymes — Taq polymerase especially. That is the problem CTAB exists to solve.

At **high salt (>0.7 M NaCl)**, CTAB binds polysaccharides but leaves nucleic acids in solution. When the salt drops, CTAB–nucleic-acid complexes precipitate instead. The protocol exploits this: extract hot in high salt so polysaccharides get bound and partitioned into the organic/interphase during [[PCI]] extraction, while DNA stays in the aqueous phase.

This is why SDS-based buffers (used for animal tissue) fail on plant material — SDS does not clear polysaccharides.

## Typical CTAB buffer composition

| Component | Typical conc. | Role |
|---|---|---|
| CTAB | 2% (w/v) | Detergent; polysaccharide complexing |
| NaCl | 1.4 M | Keeps polysaccharide–CTAB soluble, DNA free |
| Tris-HCl pH 8.0 | 100 mM | Buffers pH; DNA stable and deprotonated |
| EDTA | 20 mM | Chelates Mg²⁺ → inactivates DNases |
| [[β-mercaptoethanol]] | 0.2–2% | Reduces disulfides; blocks phenolic oxidation |

## Why 60 °C

Warm buffer keeps CTAB above its **Krafft point** (it precipitates when cold), speeds membrane lysis, and helps denature nucleases. It is not a precise-temperature step — hence "60 °C keep the solution does not matter that much" in the bench record.

## Related

- [[02_knocout_os_ctab_dna_extraction_protocol]]
- [[PCI]] · [[β-mercaptoethanol]] · [[Sodium acetate]]

```dataview
TABLE file.cday AS "Created Date"
FROM [[#]] AND -"_templates"
WHERE status = "active" OR "reference"
SORT file.cday DESC
```
