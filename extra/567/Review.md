---
type: dashboard
title: Weekly review
---
# Weekly review

## Summary
```para-zk-dashboard-summary
type: review
```

---
## Created this week: References
```dataviewjs
const pages = (source) => dv.pages(source).array();
const asArray = (value) => value == null ? [] : Array.isArray(value) ? value : (typeof value.array === 'function' ? value.array() : [value]);
const sameLink = (value, page) => value?.path === page.file.path || String(value) === String(page.file.link) || String(value) === page.file.path;
const timeOf = (value) => value?.toMillis ? value.toMillis() : new Date(value).getTime();
const dayOf = (value) => { const d = new Date(timeOf(value)); d.setHours(0,0,0,0); return d.getTime(); };
const startOfWeek = (() => { const d = new Date(); const day = (d.getDay() + 6) % 7; d.setHours(0,0,0,0); d.setDate(d.getDate() - day); return d; })();
const rows = pages("\"PARA/Resources\"")
  .filter(p => timeOf(p.file.ctime) >= startOfWeek.getTime())
  .sort((a,b) => timeOf(b.file.ctime) - timeOf(a.file.ctime))
  .map(p => [p.file.link, p.file.ctime]);
dv.table(["References", "Created"], rows);
```



---
## Created this week: Spark
```dataviewjs
const pages = (source) => dv.pages(source).array();
const asArray = (value) => value == null ? [] : Array.isArray(value) ? value : (typeof value.array === 'function' ? value.array() : [value]);
const sameLink = (value, page) => value?.path === page.file.path || String(value) === String(page.file.link) || String(value) === page.file.path;
const timeOf = (value) => value?.toMillis ? value.toMillis() : new Date(value).getTime();
const dayOf = (value) => { const d = new Date(timeOf(value)); d.setHours(0,0,0,0); return d.getTime(); };
const startOfWeek = (() => { const d = new Date(); const day = (d.getDay() + 6) % 7; d.setHours(0,0,0,0); d.setDate(d.getDate() - day); return d; })();
const rows = pages("\"ZK/Spark\"")
  .filter(p => p.processed !== true)
  .filter(p => timeOf(p.file.ctime) >= startOfWeek.getTime())
  .sort((a,b) => timeOf(b.file.ctime) - timeOf(a.file.ctime))
  .map(p => [p.file.link, p.file.ctime]);
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
  .slice(0, 50)
  .map(r => [r.file.link, r.file.ctime]);
dv.table(["References", "Created"], rows);
```
