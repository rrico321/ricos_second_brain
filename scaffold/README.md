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
- 12:00 weekdays - Vault Tidy (read-only health check + Inbox flag)
- 18:00 weekdays - Vault Tidy + archive completed tasks

On demand: `sort inbox` — Cowork classifies and proposes destinations for anything sitting in `Inbox/`.

## Updating

Tell Cowork: `Check for second-brain updates`. See `UPGRADE.md` in the repo.

## More

- Repo: https://github.com/rico/rico-second-brain-poc
- Issues: open in the repo
- Skill: `obsidian-vault` (lives in Cowork, not in your vault)
