---
type: dashboard
title: Areas dashboard
---
# Areas dashboard

## Summary
```para-zk-dashboard-summary
type: areas
```

---
## Projects dashboard
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

---
## Recent updates
```dataviewjs
const pages = (source) => dv.pages(source).array();
const asArray = (value) => value == null ? [] : Array.isArray(value) ? value : (typeof value.array === 'function' ? value.array() : [value]);
const sameLink = (value, page) => value?.path === page.file.path || String(value) === String(page.file.link) || String(value) === page.file.path;
const timeOf = (value) => value?.toMillis ? value.toMillis() : new Date(value).getTime();
const dayOf = (value) => { const d = new Date(timeOf(value)); d.setHours(0,0,0,0); return d.getTime(); };
const areas = pages("\"PARA/Areas\"").filter(p => p.type === 'area');
const projects = pages("\"PARA/Projects\"").filter(p => p.type === 'project' && !p.file.path.startsWith("PARA/Archives/")).sort((a,b) => timeOf(b.file.mtime) - timeOf(a.file.mtime));
const rows = [];
for (const area of areas) {
  const matches = projects.filter(p => asArray(p.areas).some(x => sameLink(x, area)));
  if (matches.length) rows.push([area.file.link, matches[0].file.link, matches[0].file.mtime]);
}
rows.sort((a,b) => timeOf(b[2]) - timeOf(a[2]));
dv.table(["Area", "Project", "Updated"], rows);
```
