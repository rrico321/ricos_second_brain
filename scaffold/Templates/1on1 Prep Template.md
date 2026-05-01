<%*
const name = await tp.system.prompt("Direct report name");
const date = tp.date.now("YYYY-MM-DD");
const filename = date + " - 1on1";
const folderPath = "1on1s/" + name;
if (!(await app.vault.adapter.exists(folderPath))) {
  await app.vault.createFolder(folderPath);
}
await tp.file.move("/" + folderPath + "/" + filename);
-%>
---
tags: #1on1 #meeting
date: <% date %>
direct_report: <% name %>
---

# 1:1 with <% name %> - <% date %>

---

## Their Recent Wins

- (what they shipped, decided, or unblocked since last 1:1)

---

## Their Blockers / Frustrations

- (anything they raised in Slack, recent meetings, or that you've observed)

---

## Career / Growth Discussion

- (topic for this 1:1: skills, scope, role progression, feedback)

---

## Decisions Needed From Me

- (things they're waiting on you to decide)

---

## Agenda

1.
2.
3.

---

## Notes During the Meeting

-

---

## Action Items

| Action | Owner | Due |
|--------|-------|-----|
|  |  |  |

---

## Related

- [[<% name %>]]
