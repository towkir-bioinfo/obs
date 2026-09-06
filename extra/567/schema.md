---
tags:
  - type/admin
status: reference
---
# Schema

Single source of truth for the vault's controlled vocabulary. The `normalise-metadata` skill validates every note against this file and rejects values not listed here. Adding a value means editing this file first.

## Rule

- **Tags** carry classification you navigate by and that rarely changes.
- **Properties** carry state and data that change often or need sorting.

## Facets (tags)

| Facet | Cardinality | Applies to |
|---|---|---|
| `type/` | exactly 1 | every note — routes the file |
| `project/` | 0–n | any |
| `domain/` | 0–n | any |
| `method/` | 0–n | any |
| `thread/` | 0–n | any |
| `org/` | 0–n | person, admin, teaching, meeting |

Leaves are lowercase and hyphenated. Facet prefixes are singular. No tag may exist outside these six facets.

## type/ — closed vocabulary

| Tag | Folder | Meaning |
|---|---|---|
| `type/daily` | 20-Journal/Daily/YYYY | one per working day |
| `type/meeting` | 20-Journal/Meetings | one per meeting |
| `type/review` | 20-Journal/Reviews | weekly, monthly, yearly |
| `type/project` | 10-Projects | one dashboard per project |
| `type/literature` | 30-Sources | citable source |
| `type/reference` | 30-Sources | non-citable: clipped web, docs |
| `type/note` | 40-Notes | concept / permanent note |
| `type/map` | 40-Notes | MOC or thread index |
| `type/method` | 50-Lab | protocol, SOP, pipeline |
| `type/analysis` | 50-Lab | one run or experiment |
| `type/dataset` | 50-Lab | registry pointer to data |
| `type/output` | 60-Outputs | manuscript, grant, poster, talk |
| `type/person` | 70-People | one per person |
| `type/admin` | 80-Admin | institutional process, policy |
| `type/teaching` | 80-Admin | course, lecture, supervision |

## status — property, closed vocabulary

`inbox` · `active` · `waiting` · `parked` · `done` · `reference`

One vocabulary for all types. An unread paper is `inbox`; a paper read and filed is `reference`.

## project/ — one value per project

Register every project here when created. Example form: `project/<short-slug>`.

| Tag | Full name | Started | Dashboard |
|---|---|---|---|
| | | | |

## domain/ — subject areas

Slow-growing. Register before use.

| Tag | Meaning |
|---|---|
| | |

## method/ — techniques

Grows freely but must be registered.

| Tag | Meaning |
|---|---|
| | |

## thread/ — open questions spanning projects

A thread is a question you do not yet have an answer to. It closes when answered, and the closing note records the answer.

| Tag | Question | Opened | Status |
|---|---|---|---|
| | | | |

## org/ — institutions

| Tag | Full name |
|---|---|
| | |

## Inline fields (Dataview)

Written in context, never in a dedicated section. Rolled up by project dashboards.

| Field | Written where | Meaning |
|---|---|---|
| `decision::` | daily, meeting | a choice made, with reason |
| `next::` | anywhere | a concrete next action |
| `question::` | anywhere | an open question |
| `result::` | analysis, daily | an empirical outcome |
| `blocked::` | anywhere | something preventing progress |
| `risk::` | anywhere | a foreseeable failure mode |
| `idea::` | anywhere | speculative, unevaluated |

Form: `- decision:: 2026-08-15 Text of the decision. [[project-slug]]`

## Note-specific properties

| Property | Types | Notes |
|---|---|---|
| `aliases` | any | initials, short names |
| `created` | any | YYYY-MM-DD |
| `citekey` | literature | Better BibTeX key |
| `doi`, `year`, `journal` | literature | |
| `authors` | literature, output | list |
| `url`, `accessed` | reference | |
| `attendees` | meeting | list of wikilinks |
| `affiliation`, `role`, `email` | person | |
| `accession`, `path`, `checksum` | dataset | `path` relative to `../analysis/` |
| `assay`, `holder`, `generated` | dataset | |
| `inputs`, `repo-path`, `commit` | analysis | provenance triple |
| `analysis-kind` | analysis | free but registered in method/ |
| `target`, `deadline`, `authors` | output | |
| `evidence-class` | note, analysis | see below |

## evidence-class — optional, but never inferred by an agent

`computational` · `correlative` · `in-vitro` · `heterologous-in-vivo` · `native-in-vivo`

Applied by hand only. Its purpose is to stop the link graph from giving a sequence-derived inference the same weight as a validated result.

## Filenames

Forbidden characters: `: ? * " < > | \ /` and trailing dots or spaces.
Forbidden names: CON, PRN, AUX, NUL, COM1–9, LPT1–9.
Dates always `YYYY-MM-DD`. Maximum 80 characters.
Wikilink targets are never hand-typed — always autocompleted.

| Type | Pattern |
|---|---|
| daily | `2026-08-15` |
| meeting | `2026-08-15 -- Short Name` |
| review | `2026-W33`, `2026-08`, `2026` |
| project | `Project Short Name` |
| literature | `Author2023_ShortTitle` |
| person | `Surname, Forename` |
| dataset | `DS_<accession or run id>` |
| analysis | `2026-08-15_<short-slug>` |
| others | descriptive title |
