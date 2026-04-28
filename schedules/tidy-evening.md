# Schedule: Vault Tidy (Evening) + Archive

**Trigger:** `Tidy my vault and archive completed tasks`
**Cron:** `0 18 * * 1-5` (18:00 weekdays)
**Skill invoked:** `obsidian-vault` -> Vault Tidy + Archive Completed Tasks workflows

## What it does

Same health check as Tidy Noon, plus:

- Moves all `- [x]` and `- [-]` tasks from `Tasks/Tasks.md` to `Tasks/Archive/Archive.md`
- Adds `✅ <today>` to each archived task
- Updates `Tasks/Tasks.md` `Last Updated` stamp
- Counts items in `Inbox/` and flags if any exist: "You have N items waiting in Inbox/. Run `sort inbox` when ready."

Does NOT auto-sort Inbox content. Classification requires user input - run `sort inbox` on demand for that.

## Setup instructions for SETUP.md

```yaml
name: "Vault Tidy (Evening)"
cron: "0 18 * * 1-5"
prompt: "Tidy my vault and archive completed tasks"
```
