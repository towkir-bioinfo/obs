---
tags:
  - type/daily
status: active
created: <% tp.date.now("YYYY-MM-DD") %>
---
# <% tp.date.now("YYYY-MM-DD") %>

[[<% tp.date.now("YYYY-MM-DD", -1) %>|yesterday]] · [[<% tp.date.now("YYYY-MM-DD", 1) %>|tomorrow]] · [[Home]]

**Focus::** 

## Ship's Log
- <% tp.date.now("HH:mm") %> start of day

## Meetings today
```dataview
LIST
FROM #type/meeting
WHERE file.name >= "<% tp.date.now("YYYY-MM-DD") %>" AND file.name < "<% tp.date.now("YYYY-MM-DD", 1) %>"
```

## Due and starting
```tasks
not done
path does not include _templates
starts before tomorrow
sort by due
```

## Captured today
```dataview
TABLE WITHOUT ID field AS "", text AS "Item"
FLATTEN file.lists AS L
WHERE contains(list(L.decision, L.next, L.question, L.result, L.blocked, L.risk, L.idea), null) = false
```

## Tomorrow
- 
