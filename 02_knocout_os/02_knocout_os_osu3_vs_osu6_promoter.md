---
type: note
project: "[[02_knocout_os_moc]]"
date: 2026-08-17
tags:
  - promoter-analysis
  - gene-family
People:
  - "[[ZIS]]"
---

# OsU3 vs OsU6 promoter (rice genome editing)

In rice genome editing, the **U6 promoter** (specifically `OsU6`) is generally
considered better and achieves higher mutation and editing frequencies than
the **U3 promoter** (`OsU3`).

## Key differences for rice genome editing

- **Editing efficiency**: Comparative studies in rice demonstrate that sgRNAs
  driven by the `OsU6` promoter consistently yield higher targeted
  mutagenesis rates than those driven by `OsU3`. (source: NIH)
- **Transcription start site**:
  - `U6` promoters require a 5′-guanine (G) to initiate transcription.
  - `U3` promoters require a 5′-adenine (A) to initiate transcription. (source: NIH)
- **Guide RNA design constraint**: Because standard CRISPR sgRNAs function
  reliably when matching the natural transcription initiation rules of `U6`,
  designing spacers with a leading `G` is straightforward and widely
  optimized for rice vectors.

## Source

![[Pasted image 20260817145927.png]]

> [!warning] Citations not verified
> The screenshot cites "National Institutes of..." (truncated) as the source
> for the editing-efficiency and transcription-start-site claims. The full
> citation was cut off in the capture — track down the actual paper/resource
> before relying on this for a protocol or thesis text.
