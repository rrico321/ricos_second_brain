# rico-second-brain-poc

Foundation for any Kipu Health employee (or external user) to spin up a personal AI-assisted second brain using Claude Cowork and Obsidian. Bring an empty vault. Run the bootstrap. End up with a personalized `CLAUDE.md`, three scheduled assistants, and a working knowledge graph in 10-15 minutes.

## Status

Alpha. v1.0.4. Internal-use repo, hosted on GitHub for distribution. Stress-testing with a small group before broader Kipu rollout.

## Current Status (what's real vs planned)

| Capability | State |
|---|---|
| Fresh vault bootstrap via `SETUP.md` | ✅ Works now |
| Vault scaffold (folders, templates, base subheaders) | ✅ Works now |
| Three schedules (Morning Summary, Vault Tidy Noon, Vault Tidy Evening) | ✅ Works now |
| `obsidian-vault` skill behaviour (notes, tasks, daily summaries, meeting notes, lint, archive, sort inbox) | ✅ Works now |
| Compliance guardrails (HIPAA / PHI / BAA hard-rules) | ✅ Works now |
| Org-shared skill via Kipu Cowork tenant | ⚠️ Internal-only |
| Approved Kipu connectors (Slack, M365, Atlassian, etc.) | ⚠️ Internal-only |
| Automated update flow (`cowork check for second-brain updates`) | ❌ Not yet implemented (see UPGRADE.md) |
| Auto-backup on update (`.scaffold-backup/<old-version>/`) | ❌ Not yet implemented |
| Rollback workflow | ❌ Not yet implemented |
| PR-driven skill source updates | ❌ Not yet implemented (skill source not yet in this repo) |

For v1.0.x, manual rollback uses OneDrive version history. The automated update flow lands in v1.x.

## Who this is for

- Primary: Kipu Health employees with access to a Cowork plan where the `obsidian-vault` skill has been shared org-wide
- Secondary: External users (manual `.skill` install from `releases/` via claude.ai)

## What you get

- An Obsidian vault scaffold with sensible folders and templates
- A personalized `CLAUDE.md` that routes Cowork to the right skill for each task
- Three scheduled assistants: morning summary, midday Vault Tidy, evening Vault Tidy with archive
- The `obsidian-vault` skill that knows your conventions, naming, plugin syntax, and maintenance workflows
- A `Compliance.md` guardrail referenced from `CLAUDE.md` so the agent reads org rules first

## Quick start

1. Install Obsidian (https://obsidian.md)
2. Create an empty vault on Microsoft 365 / OneDrive (Kipu employees) 
3. In Obsidian, open **Settings → Community plugins**, turn on Community plugins, and install + enable these four:
   - **Dataview** — query notes like a database
   - **Tasks** — task syntax with due dates, priority, and queries
   - **Templater** — dynamic note templates (powers Daily/Meeting/Bug/Task templates)
   - **Calendar** — daily-note navigation
   - Optional: **Excalidraw** (sketches and diagrams). The skill knows how to use it if installed.
1. Open Cowork and point it at the vault folder
2. Tell Cowork: `Go to https://github.com/rrico321/ricos_second_brain and run SETUP.md`

That is the full install. The rest is Cowork's job.

## What this is not

- Not a replacement for any existing Kipu tool
- Not a centralized PHI store. Hard hold on PHI until Anthropic BAA is signed.
- Not auto-installed. The user (or org admin) opts in.
- Not opinionated about your role. The interview adapts the scaffold to you.

## Documentation

- `SETUP.md` - the bootstrap script Cowork reads
- `UPGRADE.md` - how updates work (three-tier model)
- `COMPLIANCE.md` - HIPAA / no-PHI / BAA gap rules
- `CHANGELOG.md` - what's in each version
- `CONTRIBUTING.md` - how to suggest changes
- `docs/how-it-works.md` - architecture explainer
- `docs/vault-anatomy.md` - folder-by-folder tour of what lives in your vault and why
- `docs/faq.md` - common questions
- `docs/troubleshooting.md` - install issues
- `docs/connectors-approved.md` - Kipu-approved connector list

## License

Internal use only at Kipu Health and personal use of original author. No external distribution without permission. See `LICENSE`.
