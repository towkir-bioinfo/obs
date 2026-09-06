---
tags:
  - type/project
status: active
created: <% tp.date.now("YYYY-MM-DD") %>
started: <% tp.date.now("YYYY-MM-DD") %>
deadline: 
---
# <% tp.file.title %>

> [!info] Set the project tag below, then replace `CHANGEME` in every query.

**Tag::** #project/CHANGEME

## Where I am
<!-- the only hand-written section -->


## Blocked
```dataview
TABLE WITHOUT ID L.text AS "Blocked", file.link AS "From"
FLATTEN file.lists AS L
WHERE L.blocked AND contains(file.etags, "#project/CHANGEME")
SORT file.mtime DESC
```

## Next actions
```dataview
TABLE WITHOUT ID L.text AS "Next", file.link AS "From"
FLATTEN file.lists AS L
WHERE L.next AND contains(file.etags, "#project/CHANGEME")
SORT file.mtime DESC
```

## Open tasks
```tasks
not done
tag includes #project/CHANGEME
sort by due
```

## Decision log
```dataview
TABLE WITHOUT ID L.text AS "Decision", file.link AS "Source"
FLATTEN file.lists AS L
WHERE L.decision AND contains(file.etags, "#project/CHANGEME")
SORT file.mtime DESC
```

## Open questions
```dataview
TABLE WITHOUT ID L.text AS "Question", file.link AS "From"
FLATTEN file.lists AS L
WHERE L.question AND contains(file.etags, "#project/CHANGEME")
SORT file.mtime DESC
```

## Results
```dataview
TABLE WITHOUT ID L.text AS "Result", file.link AS "From"
FLATTEN file.lists AS L
WHERE L.result AND contains(file.etags, "#project/CHANGEME")
SORT file.mtime DESC
```

## Risks and ideas
```dataview
TABLE WITHOUT ID L.text AS "Item", file.link AS "From"
FLATTEN file.lists AS L
WHERE (L.risk OR L.idea) AND contains(file.etags, "#project/CHANGEME")
SORT file.mtime DESC
```

## Everything in this project
```dataview
TABLE WITHOUT ID file.link AS "Note", status AS "Status", file.mtime AS "Modified"
FROM #project/CHANGEME
SORT file.mtime DESC
```

## Meetings
```dataview
LIST
FROM #project/CHANGEME AND #type/meeting
SORT file.name DESC
```

## Data and analyses
```dataview
TABLE WITHOUT ID file.link AS "Note", analysis-kind AS "Kind", status AS "Status"
FROM #project/CHANGEME AND (#type/analysis OR #type/dataset)
SORT file.name DESC
```

## Outputs
```dataview
TABLE WITHOUT ID file.link AS "Output", status AS "Status", deadline AS "Deadline"
FROM #project/CHANGEME AND #type/output
```

## Recent activity
```dataview
TABLE WITHOUT ID file.link AS "Note", file.mtime AS "Touched"
FROM #project/CHANGEME
SORT file.mtime DESC
LIMIT 15
```
