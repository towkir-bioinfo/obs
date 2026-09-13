---
type: moc
project: 04_cblast
role: admin-panel
status: active
prepared_by: Towkir Hasan
updated: 2026-09-08
tags:
  - meta
  - cblast
  - admin
---

# cBLAST — Admin Panel

> [!abstract] Scope
> Operational hub for cBLAST programme administration: session register, enrolment
> figures, reports, recurring duties, and open tasks. Everything filed under
> `04_cblast/` rolls up here.

## ⚡ Quick actions

- [[cblast Annual report]] — current enrolment report *(update at each session close)*
- New session log → create `cblast Session-NN log.md`
- New report → create `cblast <period> report.md` with `type: report`
- New person/instructor → create `cblast <name>.md` with `type: person`

## 📊 Status snapshot

> [!summary] Enrolment (as of 2026-09-08 — from [[cblast Annual report]])
> | Metric | Value |
> | --- | ---: |
> | Cumulative students | **516** |
> | Cumulative re-enrolments | **151** |
> | Active session | **24th** (15 Sep – 15 Dec 2026) |
> | Previous session | 23rd (15 Jun – 15 Aug 2026) — 3 new, 1 re-enrol |

*Keep this block in sync with the headline callout in [[cblast Annual report]].*

## 🗓 Session register

| Session | Period | New | Re-enrol | Status |
| ---: | --- | ---: | ---: | --- |
| ≤22nd | Historical baseline | 503 | 150 | Closed |
| 23rd | 15 Jun – 15 Aug 2026 | 3 | 1 | Closed |
| 24th | 15 Sep – 15 Dec 2026 | 10 | 0 | **Active** |

## 📁 Reports & documents

```dataview
TABLE report AS "Report", status AS Status, as_of AS "As of", file.mtime AS Updated
FROM "04_cblast"
WHERE type = "report"
SORT as_of DESC
```

- [[cblast_annual_report_24th_session]] — raw per-course, per-session enrolment table (the source data [[cblast Annual report]] is built from); no `type` frontmatter so it doesn't appear in the table above
- [[cBLAST কোর্সের সেশন অগ্রগতি প্রতিবেদন]] — Bangla-language progress summary. ⚠️ Numbers don't match the English report: says 24th session has **16** current students (report says 10 new) and adds a figure not tracked elsewhere — **134** cumulative certificate holders. Reconcile before citing either.
- [[Know_About_cBLAST]] — course catalogue reference: full course list + per-module fee schedule
- [[cBLAST Pad - Copy]] — 23 Aug 2026 permission-request letter (poster display, NSU Biochemistry & Biotechnology dept.)

## 🗂 Everything in this area (auto)

```dataview
TABLE type AS Type, status AS Status, file.mtime AS Updated
FROM "04_cblast"
WHERE file.name != this.file.name
SORT file.mtime DESC
```

## 🕑 Recently updated

```dataview
TABLE file.mtime AS Updated
FROM "04_cblast"
WHERE file.name != this.file.name
SORT file.mtime DESC
LIMIT 5
```

## ✅ Open tasks (auto)

```dataview
TASK
FROM "04_cblast"
WHERE !completed
```

## 🔁 Recurring admin duties

- At session open: create the session log, record start/end dates, set targets
- Mid-session: update in-progress counts with an "as of" date
- At session close: finalise counts, re-sum cumulative totals, set report `status: final`
- After close: roll the finished session into the register above and start the next

---

> [!note]- Maintaining this panel
> - **Status snapshot** and **Session register** are hand-maintained — update them whenever [[cblast Annual report]] changes.
> - The three dataview blocks are automatic; they pick up any note in `04_cblast/` (reports need `type: report` to appear in the Reports table).
> - Bump `updated:` in the frontmatter when you edit the hand-maintained sections.
