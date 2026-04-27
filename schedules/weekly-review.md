# Schedule: Weekly Review

**Trigger:** `Run my weekly review`
**Cron:** `0 16 * * 5` (16:00 Friday)
**Skill invoked:** `obsidian-vault` -> Weekly Review workflow

## What it does

End-of-week summary:

- Lists tasks completed this week
- Lists tasks added this week
- Notes project status changes
- Surfaces stale items
- Appends a memory.md entry summarizing the week

## Setup instructions for SETUP.md

```yaml
name: "Weekly Review"
cron: "0 16 * * 5"
prompt: "Run my weekly review"
```
