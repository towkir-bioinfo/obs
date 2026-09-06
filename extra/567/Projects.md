---
type: dashboard
title: Projects dashboard
---
# Projects dashboard

## Summary
```para-zk-dashboard-summary
type: projects
```

---
## Due within 7 days
```dataview
TABLE WITHOUT ID file.link AS "Project", priority AS "Priority", due_date AS "Due date"
FROM "PARA/Projects"
WHERE type = "project" AND !startswith(file.path, "PARA/Archives/") AND due_date AND date(due_date) <= date(today) + dur(7 days)
SORT due_date ASC
LIMIT 50
```

---
## Due within 30 days
```dataviewjs
const pages = (source) => dv.pages(source).array();
const asArray = (value) => value == null ? [] : Array.isArray(value) ? value : (typeof value.array === 'function' ? value.array() : [value]);
const sameLink = (value, page) => value?.path === page.file.path || String(value) === String(page.file.link) || String(value) === page.file.path;
const timeOf = (value) => value?.toMillis ? value.toMillis() : new Date(value).getTime();
const dayOf = (value) => { const d = new Date(timeOf(value)); d.setHours(0,0,0,0); return d.getTime(); };
const days = (n) => 1000 * 60 * 60 * 24 * n;
const today = new Date(); today.setHours(0,0,0,0);
const projects = pages("\"PARA/Projects\"").filter(p => p.type === 'project' && !p.file.path.startsWith("PARA/Archives/") && p.due_date);
const rows = projects.filter(p => { const diff = dayOf(p.due_date) - today.getTime(); return diff > days(7) && diff <= days(30); })
  .sort((a,b) => dayOf(a.due_date) - dayOf(b.due_date))
  .map(p => [p.file.link, p.priority ?? '', p.due_date]);
dv.table(["Project", "Priority", "Due date"], rows);
```

---
## Recent updates
```dataview
TABLE WITHOUT ID file.link AS "Project", file.mtime AS "Updated", due_date AS "Due date", priority AS "Priority"
FROM "PARA/Projects"
WHERE type = "project" AND !startswith(file.path, "PARA/Archives/")
SORT file.mtime DESC
LIMIT 10
```

---
## Area
```dataviewjs
const pages = (source) => dv.pages(source).array();
const asArray = (value) => value == null ? [] : Array.isArray(value) ? value : (typeof value.array === 'function' ? value.array() : [value]);
const sameLink = (value, page) => value?.path === page.file.path || String(value) === String(page.file.link) || String(value) === page.file.path;
const timeOf = (value) => value?.toMillis ? value.toMillis() : new Date(value).getTime();
const dayOf = (value) => { const d = new Date(timeOf(value)); d.setHours(0,0,0,0); return d.getTime(); };
const areas = pages("\"PARA/Areas\"").filter(p => p.type === 'area');
const projects = pages("\"PARA/Projects\"").filter(p => p.type === 'project' && !p.file.path.startsWith("PARA/Archives/"));
const rows = areas.map(a => {
  const count = projects.filter(p => asArray(p.areas).some(x => sameLink(x, a))).length;
  return [a.file.link, count];
}).sort((a,b) => b[1] - a[1]);
dv.table(["Area", "Projects dashboard"], rows);
```
