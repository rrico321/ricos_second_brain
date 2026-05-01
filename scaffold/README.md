# Vault README

This is your personal Obsidian vault, scaffolded by `rico-second-brain-poc`.

## Structure

```
<your vault>/
├── CLAUDE.md             Routing rules for Cowork. Personalized for you.
├── Home.md               Navigation hub. Pin this in Obsidian as your default note.
├── index.md              Full catalog of every page. Cowork reads this first.
├── README.md             This file.
├── Context/              Cowork reference files + system files (Compliance.md, .scaffold-version.yaml — don't manually edit those)
├── Templates/            Templater source files
├── Daily Notes/          YYYY-MM-DD.md
├── Meeting Notes/        YYYY-MM-DD - Title.md
├── Projects/             ProjectName.md
├── People/               FirstName LastName.md
├── SOPs/                 SOP - Title.md
├── Issues/               Bug reports, dashboards, operational issues — free-form titles
├── Inbox/                Capture-first dumping ground. Drop anything here that doesn't have an obvious home. Sort with `sort inbox`.
├── Tasks/                Active and archived task list
└── (interview-added)     Strategic Initiatives/, Stakeholders/, 1on1s/, Candidates/
```

## How to use it

1. Open Cowork and point it at this folder
2. Talk to Cowork in plain English: "I had a meeting with X, add it to my obsidian," "what are my tasks today?", "what shipped this week?"
3. Cowork uses the `obsidian-vault` skill to know your conventions

## Schedules

Three schedules run automatically (when your machine is on):

- 08:00 weekdays - Morning Summary
- 12:00 weekdays - Vault Tidy (full housekeeping pass: archive, rebuild index, sync projects, surface orphans/stale items)
- 18:00 weekdays - Vault Tidy (same pass — twice a day keeps the vault current)

On demand: `sort inbox` — Cowork classifies and proposes destinations for anything sitting in `Inbox/`.

## Updating

The automated update flow (`Check for second-brain updates`) is planned for a v1.x release and not yet implemented. For v1.0.x, watch `CHANGELOG.md` in the repo and apply notable changes manually. See `UPGRADE.md` for the planned model.

## More

- Repo: https://github.com/rico/rico-second-brain-poc
- Issues: open in the repo
- Skill: `obsidian-vault` (lives in Cowork, not in your vault)
