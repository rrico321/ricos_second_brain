# Schedule: Vault Tidy (Noon)

**Trigger:** `Tidy my vault`
**Cron:** `0 12 * * 1-5` (12:00 weekdays)
**Skill invoked:** `obsidian-vault` -> Vault Tidy workflow

## What it does

Read-only health check:

- Surfaces orphan pages (no inbound wikilinks)
- Surfaces missing pages (wikilinks to files that don't exist)
- Surfaces stale content (daily notes >14 days old, dashboards >7 days, projects with no recent updates)
- Counts items in `Inbox/` and flags if any exist: "You have N items waiting in Inbox/. Run `sort inbox` when ready."
- Reports findings without making changes

## Setup instructions for SETUP.md

```yaml
name: "Vault Tidy (Noon)"
cron: "0 12 * * 1-5"
prompt: "Tidy my vault"
```

Use `mcp__scheduled-tasks__create_scheduled_task` with these parameters.
