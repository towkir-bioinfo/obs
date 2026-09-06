---
tags:
  - type/admin
status: active
---
# Work Ledger

Maintained by the agent at the start and end of each session. Read this first.

## Active
<!-- what is genuinely in progress right now -->

Migration of the legacy vault into `vault-v0/vault/` is **executed**. 89 files filed with `type/` and `status`. Nine files remain outside deliberately, listed below.

Filed: `00-Inbox` 1 · `10-Projects` 1 · `20-Journal/Daily/2026` 4 · `20-Journal/Meetings` 3 · `30-Sources` 1 · `40-Notes` 19 · `50-Lab` 13 · `60-Outputs` 1 · `70-People` 6 · `80-Admin` 21 · `90-Attachments` 19.

- next:: Rewrite the Auto Note Mover rules for the new vocabulary (see below).

### Auto Note Mover is now misconfigured

`.obsidian/plugins/auto-note-mover/data.json` is set to Automatic with nine rules mapping the retired tags to the retired folders: `#people`→`People`, `#concept`→`Concepts`, `#daily`→`Daily`, `#meeting`→`Meeting`, `#script`→`Scripts`, `#solve`→`Solves`, `#p6713`→`00_Projects/…`, `#n501mm`→`University/…/Notes`, `#c501mm`→`University/…/Cards`.

None of those tags or folders now exist. The plugin will not file anything until the rules are rewritten to route `type/` tags to the numbered folders. `CLAUDE.md` depends on this mover working.

During migration the plugin actively fought the operation: it grabbed `HMMER.md` between its move and its retag, and Obsidian wrote a stale cached `gff.md` back into `Concepts/`. Both repaired. The working order is **strip the legacy tag in place first, then move** — once no rule matches, the plugin leaves the file alone.

### Held back deliberately

| File(s) | Reason |
|---|---|
| `Solves/Master Password & Account List.md` | credentials; belongs in `_private/`, prohibition 6 |
| `00_Zettelkasten/Inbox/Over all loan and money.md` | personal finances; same |
| `00_Zettelkasten/Excalidraw/` (2) | schema defines no `type/` or folder for drawings |
| `Home.md`, `Rules.md`, `Papers.base`, `SOLVES.base`, `folder_structure.txt` | superseded by this vault's `Home.md` and `_bases/`, but deletion was never explicitly approved |

`[[c2 sc]]` in `80-Admin/SC-class 02.md` points at a held-back Excalidraw file. It resolves today because the Obsidian vault root is still `Towkirs_Vault/`. It breaks the moment `vault-v0/vault/` is opened as its own vault. Same applies to any link into the other held-back files.

### Known deviations and judgment calls

1. Person filenames kept informal (`hapsa`, `ZIS`, `tomalika apu`) against the schema's `Surname, Forename`. Approved.
2. `2026-08-06 -- Reagent Procurement` dated from its first commit (`8af4cb2`); the note carried no date.
3. `2026-08-04_e01p001-day-1-log` dated from the 2026-08-04 daily note linking it at 12:13.
4. `quality control` typed `type/teaching` as a lecture-recording note. Not derived from the source.
5. Legacy `Status` values collapsed: `active`→`active`, `inactive` and `archived`→`reference`.
6. Legacy `Areas` / `Projectes` / `Experiment` / `Key Words` properties preserved verbatim on every migrated note. They carry the project and domain links that become facet tags in the parked pass.
7. `#p6713` and `#n501mm` preserved under a `legacy-tags` property rather than dropped.
8. Inline `#c501mm` tags remain in the bodies of the 501 Cards. They sit outside the six facets and were not stripped.

### Dangling links

Pre-existing, not caused by migration: `BR75`, `BR81`, `GRAVY`, `MEME`, `NCBI CDD`, `PF0268`, `ProtParam`, `germination`, `Homolog finder Bash Script`, `BR 67 Functional Genomics--wet lab (Project)`. Each is referenced but was never created.

## Waiting on others
<!-- blocked externally; who and since when -->

`Solves/Master Password & Account List.md` has been tracked since 2026-08-11 (commit `33de3a2`) and that commit is on `origin/main` at `github.com/towkir-bioinfo/Obsidian`. Repository visibility unverified; `gh` unavailable. If public, the credentials are exposed and require rotation. Removal from history needs `git filter-repo` plus a force-push, not a delete commit.

`.claudian/sessions/*.json` are tracked and contain full conversation transcripts. They would be pushed on the next sync.

- next:: Confirm repository visibility; rotate credentials if public; add `.claudian/` to `.gitignore`.

## Parked
<!-- deliberately paused, with the reason and the trigger to resume -->

Facet-tag enrichment (`project/`, `domain/`, `method/`). Prohibition 8 bars the agent from editing `schema.md`; prohibition 12 bars applying tags absent from it. Resumes when the human applies the proposed diff registering `project/metallothionein`, `domain/{bioinformatics, proteomics, single-cell, plant-biotech}`, `method/{hmmer, blast, seqtk, scrnaseq, mass-spec, pea}`.

The legacy `Areas` / `Projectes` / `Key Words` properties and `legacy-tags` entries are the source data for that pass.

## Next session
<!-- the single thing to start with -->

Rewrite the Auto Note Mover rules for `type/` tags, or new notes will not file.

## Last session
<!-- date, what changed, what was left unfinished -->

2026-08-16. Executed the migration in eight verified batches with Obsidian open, committing after each so any corruption stayed one `git checkout` from reversible. Commits `2be639b` through `f990efd`.

Repaired Auto Note Mover interference twice (`HMMER.md`, `gff.md` duplicate). Renamed `P001 MOC` to `Functional Genomics of Metallothionein` from the note's own alias and rewrote all 9 inbound links; old name kept as an alias. Corrected a mid-batch error where a frontmatter-only inspection missed inline `#c501mm` tags and would have cut the 501 MOC query from 15 matches to 5.

Unfinished: Auto Note Mover rules, the four held-back categories, and the parked facet pass.
