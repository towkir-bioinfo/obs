---
tags:
  - type/admin
status: reference
---
# Setup

## Plugins

**Core:** Bases, Daily Notes, Templates, Backlinks, Outgoing Links, Random Note, Unique Note Creator.

**Community:** Templater, QuickAdd, Tasks, Dataview, Auto Note Mover, Citations, Pandoc, Excalidraw, Obsidian Git.

**Theme:** Minimal.

Nothing else. Vault slowness is nearly always an unused community plugin.

## First-run settings

| Setting | Value |
|---|---|
| Files & Links → New link format | Shortest path when possible |
| Files & Links → Automatically update internal links | on |
| Files & Links → Default location for new attachments | `90-Attachments` |
| Files & Links → Excluded files | `_private` |
| Daily Notes → folder | `20-Journal/Daily` |
| Daily Notes → format | `YYYY/YYYY-MM-DD` |
| Daily Notes → template | `_templates/t-daily` |
| Templater → template folder | `_templates` |
| Templater → trigger on new file creation | on |
| Unique Note Creator → format | `YYYYMMDDHHmm` |
| Unique Note Creator → folder | `00-Inbox` |

Dataview: enable inline queries and inline field highlighting.

## Auto Note Mover rules

Rule type: tag. First match wins, so order does not matter here — each note carries exactly one `type/` tag.

| Tag | Destination |
|---|---|
| `type/meeting` | `20-Journal/Meetings` |
| `type/review` | `20-Journal/Reviews` |
| `type/project` | `10-Projects` |
| `type/literature` | `30-Sources` |
| `type/reference` | `30-Sources` |
| `type/note` | `40-Notes` |
| `type/map` | `40-Notes` |
| `type/method` | `50-Lab` |
| `type/analysis` | `50-Lab` |
| `type/dataset` | `50-Lab` |
| `type/output` | `60-Outputs` |
| `type/person` | `70-People` |
| `type/admin` | `80-Admin` |
| `type/teaching` | `80-Admin` |

Excluded folders: `_meta`, `_templates`, `_bases`, `_private`, `20-Journal/Daily`.

Daily notes are placed by the Daily Notes plugin, not the mover — hence the exclusion.

## QuickAdd captures

| Name | Hotkey | Target | Format |
|---|---|---|---|
| Log line | `Ctrl+Alt+L` | today's daily note, section `## Ship's Log`, bottom | `- {{DATE:HH:mm}} {{VALUE}}` |
| Next action | `Ctrl+Alt+N` | today's daily note, section `## Ship's Log`, bottom | `- next:: {{DATE:HH:mm}} {{VALUE}}` |
| Decision | `Ctrl+Alt+D` | today's daily note, section `## Ship's Log`, bottom | `- decision:: {{DATE:YYYY-MM-DD}} {{VALUE}}` |
| Keeper note | `Ctrl+Alt+K` | new unique note in `00-Inbox` | template `_templates/t-note` |

The first is the default and should account for most captures. The fourth is the exception, used only when you already have a title in mind.

## Zotero

Better BibTeX → auto-export the library to `_meta/library.bib`, keep updated on change. The Citations plugin points at that vault-relative path, which is then identical on both machines and version-controlled, so citekey drift shows up in diffs.

## Git

```
git init
git add .
git commit -m "vault v0"
git remote add origin <private remote>
git push -u origin main
```

Protocol: pull before opening Obsidian, commit and push before closing. The remote is not a backup — keep a second copy on separate media.

`_private/` is in `.gitignore` before the first commit. History is permanent; adding it later does not remove it.

## Cross-platform

`.gitattributes` sets `eol=lf`, so Windows and Linux do not produce whole-file diffs.

NTFS is case-insensitive, ext4 is case-sensitive. A link whose case does not match its target resolves on Windows and dangles on Linux. Never hand-type a wikilink; always autocomplete. Run the link check on the Linux machine weekly — it surfaces breakage Windows hides.

Windows path limit is 260 characters unless long paths are enabled. Keep filenames under 80.

## Mobile

Read-only, occasional. Pull manually; do not edit on the phone. Editing without pulling first produces a divergent history you resolve by hand.
