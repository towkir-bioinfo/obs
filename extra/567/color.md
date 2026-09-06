---
name: color
description: Mark high-value sentences by function, backlink unfamiliar terms, legend included in every output
---
INPUT
Text to tag: $ARGUMENTS
Source file: @$1

---

TASK
Apply this color-to-function system to the text above. Use ONLY these color names — no other value is valid: red, blue, green, yellow, purple, cyan.

red = Problem (the gap/issue driving the research)
green = Solution (objective answered / main finding)
blue = Methods (key technique/approach)
cyan = Data/numbers (the specific result behind the green solution)
yellow = Description/background (context, not the gap itself)
purple = Future application/direction
(no color) underline = Limitation (study's own stated weakness)
(no color) [[double brackets]] = Unfamiliar term — word-level only, 1-2 words, never a clause or sentence. Wrap the term itself to create an Obsidian backlink. Err toward marking — cheap to remove manually if already known.

OUTPUT — build in this exact order:

1. This legend block, verbatim, unchanged:

## Legend
- <mark style="background: red;">Red</mark> — Problem
- <mark style="background: green;">Green</mark> — Solution
- <mark style="background: blue;">Blue</mark> — Methods
- <mark style="background: cyan;">Cyan</mark> — Data/numbers
- <mark style="background: yellow;">Yellow</mark> — Description/background
- <mark style="background: purple;">Purple</mark> — Future application/direction
- <u>Underline</u> — Limitation
- [[Backlink]] — Unfamiliar term

2. A horizontal rule: ---

3. The tagged text, using only:
<mark style="background: COLOR;">tagged text</mark>  (COLOR = red, blue, green, yellow, purple, or cyan — nothing else)
<u>tagged text</u>  (limitation only)
[[term]]  (unfamiliar term, inline, no color)

SELECTIVITY RULE (applies to red/green/blue/cyan/yellow/purple/underline, not to [[backlinks]]):
Tag a sentence only if you'd keep it were you forced to cut everything else to one paragraph per category. Most sentences get no tag.

TARGET COUNTS (guideline, not rigid):
- ~1 sentence per category by default.
- If the paper has genuinely more than one independent problem, finding, method, or result, tag each one that clears the selectivity rule — don't skip a real second finding to hold the count at 1.
- Soft ceiling: ~12-15 total sentence-level tags for a full paper.
- Backlinks: uncapped, word-level only.

Do not force one tag per section. A section with nothing clearing the bar gets zero tags.