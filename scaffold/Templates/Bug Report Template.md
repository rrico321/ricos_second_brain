<%*
const id = await tp.system.prompt("Bug ID (e.g. 2026-0001)");
const title = await tp.system.prompt("Bug title");
const filename = "BUG-" + id + " - " + title;
await tp.file.move("/Issues/" + filename);
-%>
---
tags: #bug
Status: Open
Priority:
Reported: <% tp.date.now("YYYY-MM-DD") %>
Assigned:
---

# BUG-<% id %> - <% title %>

---

## Description

## Impact

## Root Cause

## Investigation Steps

- [ ]

## Related
