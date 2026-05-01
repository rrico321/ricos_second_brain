# Schedule: Vault Tidy (Evening)

**Trigger:** `Tidy my vault`
**Cron:** `0 18 * * 1-5` (18:00 weekdays)
**Skill invoked:** `obsidian-vault` -> Vault Tidy workflow

## What it does

Full daily housekeeping pass. Same workflow as Tidy Noon — there is no longer a "noon read-only" / "evening with archive" split. Tidy is one workflow regardless of when it runs.

**Auto-do (no user input):**
- Archive completed tasks (`[x]` and `[-]`) from `Tasks/Tasks.md` to `Tasks/Archive/Archive.md` with `✅ <today>` stamp
- Rebuild `index.md` (full vault catalog)
- Sync `Context/projects.md` with current `Projects/` files
- Update linked sections in `Home.md` (Active Projects, SOPs, Recent Meeting Notes, Team, Candidates, Templates)
- Append a Tidy summary entry to `Context/Memory.md`

**Surface for user action (no auto-changes):**
- Inbox count: "You have N items waiting in `Inbox/`. Run `sort inbox` when ready."
- Orphan pages, missing wikilinks, stale Active projects (14+ days untouched)
- Dangling tasks in today's Daily Note that look like commitments but aren't formatted as Tasks lines
- Meeting notes from past 3 days with empty Owners tables
- Frontmatter gaps (projects missing Status, candidates missing Position, etc.)
- Stale undated tasks (no `📅`, created 10+ days ago)

Tidy NEVER auto-sorts Inbox content. Classification is on-demand via the `Sort Inbox` workflow.

## Setup instructions for SETUP.md

```yaml
name: "Vault Tidy (Evening)"
cron: "0 18 * * 1-5"
prompt: "Tidy my vault"
```

Use `mcp__scheduled-tasks__create_scheduled_task` with these parameters.
