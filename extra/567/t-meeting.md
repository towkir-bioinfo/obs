---
tags:
  - type/meeting
  - org/
status: active
created: <% tp.date.now("YYYY-MM-DD") %>
aliases:
  - <% tp.file.title.split(" -- ")[1] %>
attendees: 
---
# <% tp.file.title %>

[[<% tp.file.title.split(" -- ")[0] %>|daily note]]

## Prep
<!-- written days in advance; this is the point of the note -->
- 

## Carried over
```dataview
LIST
FROM #type/meeting
WHERE contains(file.aliases, this.file.aliases[0]) AND file.name != this.file.name
SORT file.name DESC
LIMIT 3
```

## Attendees
- 

## Agenda
- 

## Notes
- 

## Out of this meeting
<!-- decision:: next:: question:: blocked:: written inline, here or above -->
- 

## Attachments
- 
