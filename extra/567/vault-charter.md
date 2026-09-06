---
tags:
  - type/admin
status: reference
---
# Vault Charter

## What this vault is for

A single career-length store for research, teaching, supervision, and institutional work. Projects come and go inside it; the vault outlives all of them. Nothing in the structure is specific to any one project.

## What it is not for

- Raw data. Sequences, alignments, BAM files, intermediates live in `../analysis/` under separate version control. This vault holds pointers, checksums, and provenance.
- Personnel records. Evaluative content about people you supervise belongs in the institutional system, not here. `_private/` exists only for material that must be recorded and must not be exposed.
- Official minutes. Meeting notes here are personal recall cues, not the record of what was decided for anyone else.

## The two states

Capture is messy and costs nothing. Retrieval is structured and costs nothing. The work between them — reading, connecting, rewriting, deciding — is yours and is not delegated.

## How organisation actually happens

You never file anything. Auto Note Mover routes on the `type/` tag, which is set by the template at creation and never changes. Everything else is found by tag, property, Bases view, or backlink. If you find yourself dragging a file, the rules are wrong — fix the rule, not the file.

## Folders

| Folder | Holds |
|---|---|
| `_meta/` | charter, schema, agent config, ledger, library.bib |
| `_templates/` | Templater templates |
| `_bases/` | Bases view definitions |
| `00-Inbox/` | unrouted capture; emptied weekly |
| `10-Projects/` | one dashboard note per project |
| `20-Journal/` | daily notes, meetings, periodic reviews |
| `30-Sources/` | literature and reference clippings |
| `40-Notes/` | concept notes and maps — the thinking layer |
| `50-Lab/` | methods, analysis runs, dataset registry |
| `60-Outputs/` | manuscripts, grants, posters, talks |
| `70-People/` | one note per person |
| `80-Admin/` | institutional process, teaching |
| `90-Attachments/` | binaries referenced by notes |
| `_private/` | agent-excluded, gitignored, unsynced |

## Daily rhythm

1. Pull, open, create today's daily note.
2. Capture everything into the Ship's Log with one hotkey. No filing, no titles.
3. Create meeting notes days ahead; the Prep section accumulates.
4. Write `next::`, `decision::`, `question::` in context, wherever you are.
5. Commit and push before closing.

## Weekly review

1. Empty `00-Inbox/`.
2. Read the week's log; promote three or four load-bearing lines into concept notes with real titles.
3. Clear stale `status: active`.
4. Run the hygiene view; fix schema violations.
5. Run the link check on the Linux machine.
6. Write the weekly review note.

## Failure modes to watch

- `00-Inbox/` stops being emptied. The system is then a folder with extra steps.
- `40-Notes/` stays empty. The vault has become a citation manager.
- Tag vocabulary drifts. Fix by editing `schema.md`, then running normalisation — never by inventing a tag in a note.
- Project dashboards get hand-edited. They are generated; only the status header is written by hand.
