# Schedule: Morning Summary

**Trigger:** `Run my morning summary`
**Cron:** `0 8 * * 1-5` (08:00 weekdays)
**Skill invoked:** `obsidian-vault` -> Morning Summary workflow

## What it does

Reads `Tasks/Tasks.md`, the most recent `Daily Notes/`, recent `Meeting Notes/`, and all active `Projects/` files. Produces a four-section output:

1. Overdue tasks
2. Tasks due within 3 days
3. Tasks with no due date created 5+ days ago
4. Project status (one line per active project)

## Setup instructions for SETUP.md

```yaml
name: "Morning Summary"
cron: "0 8 * * 1-5"
prompt: "Run my morning summary"
```

Use `mcp__scheduled-tasks__create_scheduled_task` with these parameters.
