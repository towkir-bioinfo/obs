---
type: dashboard
title: Resources dashboard
---
# Resources dashboard

## Summary
```para-zk-dashboard-summary
type: resources
```

---
## Active
```dataviewjs
const pages = (source) => dv.pages(source).array();
const asArray = (value) => value == null ? [] : Array.isArray(value) ? value : (typeof value.array === 'function' ? value.array() : [value]);
const sameLink = (value, page) => value?.path === page.file.path || String(value) === String(page.file.link) || String(value) === page.file.path;
const timeOf = (value) => value?.toMillis ? value.toMillis() : new Date(value).getTime();
const dayOf = (value) => { const d = new Date(timeOf(value)); d.setHours(0,0,0,0); return d.getTime(); };
const rows = pages("\"PARA/Resources\"")
  .filter(r => asArray(r.file.inlinks).some(l => l.path.startsWith("PARA/Projects/") || l.path.startsWith("PARA/Areas/")))
  .sort((a,b) => timeOf(b.file.mtime) - timeOf(a.file.mtime))
  .map(r => [r.file.link, asArray(r.file.inlinks).length, r.file.mtime, r.file.ctime]);
dv.table(["References", "Backlinks", "Updated", "Created"], rows);
```

---
## Unreferenced
```dataviewjs
const pages = (source) => dv.pages(source).array();
const asArray = (value) => value == null ? [] : Array.isArray(value) ? value : (typeof value.array === 'function' ? value.array() : [value]);
const sameLink = (value, page) => value?.path === page.file.path || String(value) === String(page.file.link) || String(value) === page.file.path;
const timeOf = (value) => value?.toMillis ? value.toMillis() : new Date(value).getTime();
const dayOf = (value) => { const d = new Date(timeOf(value)); d.setHours(0,0,0,0); return d.getTime(); };
const rows = pages("\"PARA/Resources\"")
  .filter(r => !asArray(r.file.inlinks).some(l => l.path.startsWith("PARA/Projects/") || l.path.startsWith("PARA/Areas/")))
  .sort((a,b) => timeOf(b.file.mtime) - timeOf(a.file.mtime))
  .map(r => [r.file.link, asArray(r.file.inlinks).length, r.file.mtime, r.file.ctime]);
dv.table(["References", "Backlinks", "Updated", "Created"], rows);
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

---
## ZK dashboard
```dataviewjs
const pages = (source) => dv.pages(source).array();
const asArray = (value) => value == null ? [] : Array.isArray(value) ? value : (typeof value.array === 'function' ? value.array() : [value]);
const sameLink = (value, page) => value?.path === page.file.path || String(value) === String(page.file.link) || String(value) === page.file.path;
const timeOf = (value) => value?.toMillis ? value.toMillis() : new Date(value).getTime();
const dayOf = (value) => { const d = new Date(timeOf(value)); d.setHours(0,0,0,0); return d.getTime(); };
const rows = pages("\"PARA/Resources\"")
  .filter(r => asArray(r.file.inlinks).some(l => l.path.startsWith("ZK/")))
  .sort((a,b) => timeOf(b.file.mtime) - timeOf(a.file.mtime))
  .map(r => [r.file.link, asArray(r.file.inlinks).length, r.file.mtime, r.file.ctime]);
dv.table(["References", "Backlinks", "Updated", "Created"], rows);
```
