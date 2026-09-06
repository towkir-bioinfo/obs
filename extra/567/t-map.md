---
tags:
  - type/map
status: active
created: <% tp.date.now("YYYY-MM-DD") %>
---
# <% tp.file.title %>

<!-- An index over a thread or domain. Hand-curated ordering; the query below catches what you missed. -->

## The question


## Curated path
1. 

## Everything tagged here
```dataview
TABLE WITHOUT ID file.link AS "Note", status AS "Status", file.mtime AS "Modified"
FROM #thread/CHANGEME
SORT file.mtime DESC
```
