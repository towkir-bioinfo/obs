---
type: daily
date: <% tp.date.now("YYYY-MM-DD") %>
tags: []
---

# <% tp.date.now("YYYY-MM-DD") %>

## Ship's log

- <% tp.date.now("HH:mm") %> — 

## Tasks

- [ ] 

## Captured

## Needs triage

```dataview
LIST
FROM "00 Inbox"
WHERE !type
SORT file.cday ASC
```
