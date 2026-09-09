---
type: protocol
project: "[[02_knocout_os_moc]]"
status: active
date: 2026-08-20
tags:
  - dna-extraction
  - ctab
  - protocols
---

# CTAB genomic DNA extraction — rice young leaf

As followed on 2026-08-20 for [[02_knocout_os_e001_pcr_mt_confirmation_t3]]. Wording kept as recorded at the bench.

> [!warning] Safety
> β-mercaptoethanol is carcinogenic — mix **outside**, gloves and mask required.
> Phenol is highly irritating — 100% gloves. Clean the desk; if phenol gets on gloves, wash hands.

## Before you start — check reagents

- CTAB available?
- Ice-cold isopropanol — if not enough, pour and put in the freezer
- PCI available? Especially **chloroform and IAA** — na thakle 24:1 ratio te chloroform:IAA deya lagbe
- Two separate pipettes — must be dry inside, wet thaka jabe na (special pipette machine ase, use kora lagbe)
- Conical for reagents — fully foil paper diye murano lagbe reagent dhalar age

> [!tip] Staffing & consumables
> Ekjon er kaj na; 2 jon hole valo — Omor vai ke lagbe ba onno keo.
> 2 mL eppendorf: pata besi thakle 2× ba 3× neya lagbe. 10 ta sample er jono 20 ta lagsilo; total 20+20+20 = 60 ta lagsilo.

## Steps

1. **12:30 — make CTAB buffer.** Take [[CTAB]] from the balance-machine side. 10 simple (20 mL buffer) → add 40 µL β-mercaptoethanol.
2. **Mix outside** (β-mercapto is carcinogenic — glove + mask).
3. **Shake it a few times.**
   > [!bug] Deviation on 2026-08-20
   > I did not follow this. The DNA mix did not come out good — this can be one reason.
4. Put on the **water bath at 60 °C** (keeping the solution exactly at temp does not matter that much). Falcon tube rack e rakha lagbe water bathe.
5. **Collect samples** from common lab 2 room, −80 freezer. Take a flask with liquid N₂ for this.
6. **Bring mortar & pestle**, clean with ethanol tissue.
7. When bath temp reaches 60 °C — **crush the leaves with liquid N₂**, then add 1–2 mL CTAB.
8. Paste jeta hobe oita eppendorf e dibo → quickly 60 °C bath e diye dibo. Do this for all samples.
   > [!tip] CTAB ta ekta bikar e 60 °C water rekhe then korle easy hoy.
9. **Every 6 min** sample gula up-down kora lagbe — so eksathe ei kora lagbe. Check the time of the 1st sample and keep a note track for every 3–5 samples (oi hisabe uthate hobe 30 min por).
10. After all samples done — **close the water bath lid**, note the time, and up-down **every 5 min**.
11. **Meanwhile prepare [[PCI]] solution** and keep shaking.
12. Open all the eppendorfs (jodi 20 ta sample hoy, then 1st e 30 min hole 10 ta tulte hobe, then 2nd 10 ta).
13. Shake the flask and **drop 1 mL** — onk slippery, so sathe sathe 1st tay dhele dite hobe.
14. After phenol addition, **mix up-down for 5 min**.
15. **Centrifuge 10,000 rpm, 4 °C, 15 min.** Based on sample size, 2–3 shapes kora lagte pare.
16. Meanwhile label more eppendorfs if not done already.
17. After 15 min — **transfer the aqueous layer** to a fresh eppendorf (this time **autoclaved**, 2 mL or 1 mL depending kototuku asche).
18. Add **1 mL chloroform + IAA** (from the bottle straight this time). Up-down 2–5 min → **10,000 rpm, 4 °C, 15 min**.
19. Two layers form: **upper = DNA**, lower = chloroform. Take **500–600 µL from the top**.
20. Add **ice-cold isopropanol (propan-2-ol), 1 mL** and **1/10 volume 3 M Na-acetate** (500 µL hole 50 µL).
21. **Store at −20 °C freezer.**

## Answered questions

- [x] **Why is [[β-mercaptoethanol]] needed?**
  Two jobs. It **reduces disulfide bonds**, denaturing proteins — including the DNases that would degrade genomic DNA the instant the cell lyses. And it **blocks phenolic oxidation**: plant cells are full of polyphenols, and on crushing, polyphenol oxidase turns them into quinones that cross-link irreversibly to DNA and protein (the sample browns, the DNA degrades and inhibits PCR). β-ME keeps them reduced so that never starts. Add it **fresh**, immediately before use — it oxidises in air.

- [x] **What is in [[CTAB]] and why is it used?**
  CTAB = cetyltrimethylammonium bromide, a cationic detergent. Buffer is typically **2% CTAB, 1.4 M NaCl, 100 mM Tris-HCl pH 8.0, 20 mM EDTA**, plus β-ME. It exists to solve the *polysaccharide* problem: plant cell wall and mucilage polysaccharides co-purify with DNA and inhibit Taq. At high salt (>0.7 M) CTAB complexes polysaccharides while leaving nucleic acids in solution, so they partition away during [[PCI]] extraction. EDTA chelates Mg²⁺ to kill DNases; Tris holds pH 8. This is why SDS buffers (fine for animal tissue) fail on plants.

- [x] **Why use 3 M [[Sodium acetate|Na-acetate]] at this step?**
  DNA's phosphate backbone is negatively charged, so strands repel and stay dissolved; alcohol alone won't drop them out. Na⁺ shields that charge, letting DNA aggregate and precipitate. 3 M at 1/10 volume gives **~0.3 M final**, the empirical optimum; pH 5.2 keeps DNA stable. Without it, yield craters.
  > [!tip] Follow-up
  > Isopropanol co-precipitates salt more than ethanol does — add a **70% ethanol wash** after precipitation to clear residual NaOAc before resuspension.

- [x] Did skipping the shake at step 3 cause the poor DNA quality? Repeat with the shake and compare.

## Still open

- [ ] Record the primer pair and expected amplicon size used for the MT transgene PCR
- [ ] Confirm whether a 70% ethanol wash is already part of the lab's standing protocol or needs adding

## Related

- [[02_knocout_os_e001_pcr_mt_confirmation_t3]]
- Reagents: [[CTAB]] · [[PCI]] · [[β-mercaptoethanol]] · [[Sodium acetate]]
- [[2026-08-20]]
