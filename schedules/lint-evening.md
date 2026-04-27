# Schedule: Vault Lint + Archive (Evening)

**Trigger:** `Run vault lint and archive completed tasks`
**Cron:** `0 18 * * 1-5` (18:00 weekdays)
**Skill invoked:** `obsidian-vault` -> Vault Lint + Archive Completed Tasks workflows

## What it does

Same lint as the noon run, plus:

- Moves all `- [x]` and `- [-]` tasks from `Tasks/Tasks.md` to `Tasks/Archive/Archive.md`
- Adds `✅ <today>` to each archived task
- Updates `Tasks/Tasks.md` `Last Updated` stamp

## Setup instructions for SETUP.md

```yaml
name: "Vault Lint (Evening)"
cron: "0 18 * * 1-5"
prompt: "Run vault lint and archive completed tasks"
```
