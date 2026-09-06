---
type: note
date: 2026-08-20
tags:
  - dna-extraction
  - reagents
legacy-status: reference
---
>[!info] Defination:
> **Phenol : Chloroform : Isoamyl alcohol**, mixed **25 : 24 : 1**, used to strip protein away from nucleic acids by phase separation. The chloroform:IAA sub-mix alone is **24 : 1**.

## What each component does

| Component | Role |
|---|---|
| **Phenol** | Denatures protein and drives it into the organic phase / interphase. At pH 8 DNA stays in the aqueous phase (at acidic pH DNA partitions into the organic phase instead — this is how RNA is selectively recovered). |
| **Chloroform** | Denatures protein, removes lipids, and increases the density difference so the phases separate cleanly and quickly. Also strips residual phenol from the aqueous layer. |
| **Isoamyl alcohol** | Anti-foaming agent. Suppresses the emulsion at the interface so the boundary is sharp and easy to pipette against. |

## Phase behaviour

After centrifugation:

- **Upper aqueous layer → DNA** (this is what you keep, 500–600 µL from the top)
- **Interphase** → denatured protein, CTAB–polysaccharide complexes
- **Lower organic layer** → phenol/chloroform, lipids

The follow-up **chloroform:IAA (24:1)** wash exists to remove carryover phenol — residual phenol inhibits PCR and skews A260/A280 readings.

> [!warning] Safety
> Phenol causes severe chemical burns and is readily absorbed through skin. Gloves at all times; wash immediately on contact. Keep the conical wrapped in foil — phenol oxidises in light, and oxidised (pink/yellow) phenol damages DNA.

## Related

- [[02_knocout_os_ctab_dna_extraction_protocol]]
- [[CTAB]] · [[β-mercaptoethanol]] · [[Sodium acetate]]

```dataview
TABLE file.cday AS "Created Date"
FROM [[#]] AND -"_templates"
WHERE status = "active" OR "reference"
SORT file.cday DESC
```
