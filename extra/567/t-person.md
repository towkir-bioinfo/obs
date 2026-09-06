---
tags:
  - type/person
  - org/
status: reference
created: <% tp.date.now("YYYY-MM-DD") %>
aliases: 
affiliation: 
role: 
email: 
---
# <% tp.file.title %>

<!-- Identity and affiliation only. Nothing evaluative. The value of this note is its backlinks. -->

## Context
- 

## Where they appear
```dataview
TABLE WITHOUT ID file.link AS "Note", file.mtime AS "Modified"
FROM [[]]
SORT file.mtime DESC
LIMIT 25
```
