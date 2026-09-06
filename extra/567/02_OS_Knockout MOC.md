---
type: moc
project: 02_OS_Knockout
status: active
date: 2026-08-20
tags:
  - meta
  - oryza-sativa
  - crispr
  - knockout
---

# 02_OS_Knockout — MOC

> [!info] Scope
> CRISPR/Cas9 knockout work in *Oryza sativa*.

## Folder map

| #   | Folder                 | Holds                                                                           |
| --- | ---------------------- | ------------------------------------------------------------------------------- |
| 00  | [[00_planning]]        | proposal_grant, budget_timeline, ethics_biosafety_approval                      |
| 01  | [[01_protocols_SOPs]]  | bench + dry-lab SOPs                                                            |
| 02  | [[02_raw_data]]        | sequencing, qPCR_expression, microscopy, gel_western_images, instrument_exports |
| 03  | [[03_sample_metadata]] | sample sheets, accessions, conditions                                           |
| 04  | [[04_processed_data]]  | cleaned/derived matrices                                                        |
| 05  | [[05_analysis]]        | phylogenetics, promoter_analysis, scripts_code, statistics                      |
| 06  | [[06_figures]]         | source_editable, final_print_ready                                              |
| 07  | [[07_manuscript]]      | drafts, supplementary_files, submission_package, reviewer_responses             |
| 08  | [[08_presentations]]   | lab_meetings, conference_talks, posters                                         |
| 09  | [[09_literature]]      | 1st Pass, 2nd Pass, 3rd Pass                                                    |
| 10  | [[10_lab_notebook]]    | dated bench entries                                                             |
| 11  | [[11_data_deposit]]    | sequence_repository, dataset_repository                                         |
| —   | [[archive_backup]]     | superseded material                                                             |

## Everything in this project

```dataview
TABLE type AS Type, status AS Status, file.folder AS Folder, file.mtime AS Touched
FROM "01_Projects/02_OS_Knockout"
WHERE file.name != this.file.name
SORT file.mtime DESC
```

## Experiments

```dataview
TABLE stage AS Stage, iteration AS Iter, status AS Status, file.mtime AS Touched
FROM "01_Projects/02_OS_Knockout"
WHERE type = "experiment"
SORT stage ASC
```

## Literature by pass

```dataview
TABLE citekey AS Key, year AS Year, status AS Status
FROM "01_Projects/02_OS_Knockout/09_literature"
WHERE type = "paper"
SORT year DESC
```

## Lab notebook — latest

```dataview
TABLE file.cday AS Created
FROM "01_Projects/02_OS_Knockout/10_lab_notebook"
SORT file.cday DESC
LIMIT 15
```

## Open tasks

```dataview
TASK
FROM "01_Projects/02_OS_Knockout"
WHERE !completed
```

## Log

- [ ] Lock the guide-RNA design + promoter choice (see [[02_knocout_os_osu3_vs_osu6_promoter]]) before cloning
