---
type: dashboard
title: Home
---
# Home

```para-zk-dashboard-actions
```

## Summary
```para-zk-dashboard-summary
type: home
```

---
## Due within 7 days
```dataview
TABLE WITHOUT ID file.link AS "Project", priority AS "Priority", due_date AS "Due date"
FROM "PARA/Projects"
WHERE type = "project" AND !startswith(file.path, "PARA/Archives/") AND due_date AND date(due_date) <= date(today) + dur(7 days)
SORT due_date ASC
LIMIT 15
```

---
## Today's tasks
```para-zk-tasks
root: all
checkbox: open
due: today
limit: 10
```

---
## Next 7 days
```para-zk-tasks
root: all
checkbox: open
due: upcoming7
limit: 10
```

---
## Recent updates
```dataview
TABLE WITHOUT ID file.link AS "References", choice(type = "project", "Project", choice(type = "area", "Area", choice(type = "resource", "Resource", choice(type = "spark", "Spark", choice(type = "digest", "Digest", choice(type = "permanent", "Permanent", choice(type = "llm-wiki", "LLM-Wiki", type))))))) AS "Type", file.mtime AS "Updated"
FROM "PARA/Projects" OR "PARA/Areas" OR "PARA/Resources" OR "ZK"
WHERE (type = "project" OR type = "area" OR type = "resource" OR type = "spark" OR type = "digest" OR type = "permanent") AND !startswith(file.path, "PARA/Archives/")
SORT file.mtime DESC
LIMIT 10
```

---
## Independent resources
```dataviewjs
const pages = (source) => dv.pages(source).array();
const asArray = (value) => value == null ? [] : Array.isArray(value) ? value : (typeof value.array === 'function' ? value.array() : [value]);
const sameLink = (value, page) => value?.path === page.file.path || String(value) === String(page.file.link) || String(value) === page.file.path;
const timeOf = (value) => value?.toMillis ? value.toMillis() : new Date(value).getTime();
const dayOf = (value) => { const d = new Date(timeOf(value)); d.setHours(0,0,0,0); return d.getTime(); };
const rows = pages("\"PARA/Resources\"")
  .filter(r => asArray(r.file.inlinks).length === 0)
  .sort((a,b) => timeOf(b.file.ctime) - timeOf(a.file.ctime))
  .slice(0, 10)
  .map(r => [r.file.link, r.file.ctime]);
dv.table(["References", "Created"], rows);
```

---
## Waiting 7+ days
```dataviewjs
const pages = (source) => dv.pages(source).array();
const asArray = (value) => value == null ? [] : Array.isArray(value) ? value : (typeof value.array === 'function' ? value.array() : [value]);
const sameLink = (value, page) => value?.path === page.file.path || String(value) === String(page.file.link) || String(value) === page.file.path;
const timeOf = (value) => value?.toMillis ? value.toMillis() : new Date(value).getTime();
const dayOf = (value) => { const d = new Date(timeOf(value)); d.setHours(0,0,0,0); return d.getTime(); };
const days = (n) => 1000 * 60 * 60 * 24 * n;
const now = Date.now();
const rows = pages("\"ZK/Spark\"")
  .filter(f => f.processed !== true)
  .filter(f => now - timeOf(f.file.ctime) >= days(7))
  .sort((a,b) => timeOf(a.file.ctime) - timeOf(b.file.ctime))
  .slice(0, 10)
  .map(f => [f.file.link, f.file.ctime]);
dv.table(['Spark', "Created"], rows);
```

## Refinement candidates
```dataviewjs
const pages = (source) => dv.pages(source).array();
const asArray = (value) => value == null ? [] : Array.isArray(value) ? value : (typeof value.array === 'function' ? value.array() : [value]);
const sameLink = (value, page) => value?.path === page.file.path || String(value) === String(page.file.link) || String(value) === page.file.path;
const timeOf = (value) => value?.toMillis ? value.toMillis() : new Date(value).getTime();
const dayOf = (value) => { const d = new Date(timeOf(value)); d.setHours(0,0,0,0); return d.getTime(); };
const days = (n) => 1000 * 60 * 60 * 24 * n;
const now = Date.now();
const rows = pages("\"ZK/Permanent\"")
  .filter(p => p.maturity === 'draft' && now - timeOf(p.file.mtime) >= days(14))
  .sort((a,b) => timeOf(a.file.mtime) - timeOf(b.file.mtime))
  .slice(0, 10)
  .map(p => [p.file.link, p.file.mtime]);
dv.table(['Permanent', "Updated"], rows);
```
