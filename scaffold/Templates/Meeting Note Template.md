<%*
const date = tp.date.now("YYYY-MM-DD");
const title = await tp.system.prompt("Meeting title");
const filename = date + " - " + title;
await tp.file.move("/Meeting Notes/" + filename);
-%>
---
tags: #meeting
date: <% date %>
attendees:
---

# <% date %> - <% title %>

---

## Subject

---

## Key Takeaways

-

---

## Owners

| Action | Owner | Due |
|--------|-------|-----|
|  |  |  |

---

## Related
