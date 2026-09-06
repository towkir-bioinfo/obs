---
tags:
  - type/review
status: active
created: <% tp.date.now("YYYY-MM-DD") %>
period: week
---
# <% tp.date.now("gggg-[W]WW") %>

## Inbox
```dataview
LIST
FROM "00-Inbox"
SORT file.ctime ASC
```

## This week's log
```dataview
LIST
FROM #type/daily
WHERE file.day >= date(today) - dur(7 days)
SORT file.name DESC
```

## Promote
<!-- three or four log lines that deserve a real note with a real title -->
- 

## Stale actives
```dataview
TABLE WITHOUT ID file.link AS "Note", file.mtime AS "Last touched"
WHERE status = "active" AND file.mtime < date(today) - dur(21 days)
SORT file.mtime ASC
```

## Decisions this week
```dataview
TABLE WITHOUT ID L.text AS "Decision", file.link AS "Source"
FLATTEN file.lists AS L
WHERE L.decision AND file.mtime >= date(today) - dur(7 days)
```

## Next week
- 
