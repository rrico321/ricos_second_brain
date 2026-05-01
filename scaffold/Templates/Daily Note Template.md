<%*
const date = tp.date.now("YYYY-MM-DD");
const targetPath = "Daily Notes/" + date + ".md";
if (await tp.file.exists(targetPath)) {
  new Notice(`⚠️ Daily note for ${date} already exists. Opening it — this template won't overwrite.`);
  await app.vault.delete(tp.config.target_file);
  const existing = app.vault.getAbstractFileByPath(targetPath);
  if (existing) await app.workspace.getLeaf().openFile(existing);
  return;
}
await tp.file.move("/Daily Notes/" + date);
-%>
---
tags: #daily
date: <% date %>
---

# Daily Note - <% tp.date.now("YYYY-MM-DD, dddd") %>

---

## Focus Today

-

---

## Notes

-

---

## Tomorrow / Follow-up

-

---

## Open Tasks

```tasks
not done
path does not include Archive
sort by urgency
sort by due date
hide task count
hide backlink
```
