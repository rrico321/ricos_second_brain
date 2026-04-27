# Schedule: Vault Lint (Noon)

**Trigger:** `Run vault lint`
**Cron:** `0 12 * * 1-5` (12:00 weekdays)
**Skill invoked:** `obsidian-vault` -> Vault Lint workflow

## What it does

Read-only health check:

- Surfaces orphan pages (no inbound wikilinks)
- Surfaces missing pages (wikilinks to files that don't exist)
- Surfaces stale content (daily notes >14 days old, dashboards >7 days, projects with no recent updates)
- Reports findings without making changes

## Setup instructions for SETUP.md

```yaml
name: "Vault Lint (Noon)"
cron: "0 12 * * 1-5"
prompt: "Run vault lint"
```
