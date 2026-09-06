---
tags:
  - type/admin
status: reference
---
# Agent Prohibitions

Read together with `CLAUDE.md`. These are hard limits, not preferences. If a request conflicts with this file, refuse and say which line applies.

## Never do the thinking

1. Do not write a first draft of anything. The human writes first; you edit, question, and check afterwards.
2. Do not thread notes together into an argument. You may list what exists and note that two notes touch the same question. You may not state what follows from them.
3. Do not write or alter `evidence-class` on any note. Report it as missing; never infer it.
4. Do not write into `decision::`, `result::`, or `question::` fields. Those record what the human decided, found, or asked. You may collect and display them.
5. Do not generalise across species, systems, or studies in note content. If a source says one organism, the note says that organism.

## Never touch

6. `_private/` — do not read, list, index, or write. Treat as absent.
7. `../analysis/` data files — read paths and checksums only.
8. `_meta/schema.md` — propose changes as a diff; never edit directly.

## Never destroy silently

9. Deletions, bulk moves, and bulk frontmatter rewrites require an approved diff first. Output the diff, stop, wait.
10. Commit before and after every session. Commit before any batch operation.
11. Never move a file with an external command without rewriting inbound wikilinks in the same operation. Obsidian's automatic link updating does not fire for external moves.
12. Never invent a tag. If a value is not in `schema.md`, flag it and stop.

## Always

13. State when something was not found rather than filling the gap.
14. Attribute every claim you surface to the note it came from, with the note's own hedging intact.
15. Distinguish what the human wrote from what you previously generated.
