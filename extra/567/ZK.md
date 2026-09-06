---
type: dashboard
title: ZK dashboard
---
# ZK dashboard

## Summary
```para-zk-dashboard-summary
type: zk
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
  .slice(0, 50)
  .map(f => [f.file.link, f.file.ctime]);
dv.table(['Spark', "Created"], rows);
```

---
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
  .slice(0, 50)
  .map(p => [p.file.link, p.file.mtime]);
dv.table(['Permanent', "Updated"], rows);
```

---
## Recently created
```dataview
TABLE WITHOUT ID file.link AS "Digest", file.ctime AS "Created", file.mtime AS "Updated"
FROM "ZK/Digest"
SORT file.ctime DESC
LIMIT 10
```
