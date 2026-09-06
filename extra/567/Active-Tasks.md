---
type: note
date: 2026-08-24
tags:
  - meta
---

# Active Tasks

Live view — every open task across the vault, pulled by query rather than maintained by hand.

```dataview
TASK
FROM ""
WHERE !completed AND !contains(file.path, "99_Archives")
GROUP BY file.link
```

## See also

- [[Active.base]] — filterable table view of everything with `status == "active"`
- [[Recurring-Schedule]]
- [[OKR-Current]]
