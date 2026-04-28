# rico-second-brain-poc

Foundation for any Kipu Health employee (or external user) to spin up a personal AI-assisted second brain using Claude Cowork and Obsidian. Bring an empty vault. Run the bootstrap. End up with a personalized `CLAUDE.md`, four scheduled assistants, and a working knowledge graph in 10-15 minutes.

## Status

Alpha. v1.0.0. Private until stress-tested with Chris Duncombe and Nikki Kent. Targeting May ELT demo.

## Who this is for

- Primary: Kipu Health employees with access to a Cowork plan where the `obsidian-vault` skill has been shared org-wide
- Secondary: External users (manual `.skill` install from `releases/` via claude.ai)

## What you get

- An Obsidian vault scaffold with sensible folders and templates
- A personalized `CLAUDE.md` that routes Cowork to the right skill for each task
- Four scheduled assistants: morning summary, midday lint, evening lint with archive, weekly review
- The `obsidian-vault` skill that knows your conventions, naming, plugin syntax, and maintenance workflows
- A `Compliance.md` guardrail referenced from `CLAUDE.md` so the agent reads org rules first

## Quick start

1. Install Obsidian (https://obsidian.md)
2. Create an empty vault on Microsoft 365 / OneDrive (Kipu employees) or iCloud (personal)
3. Open Cowork and point it at the vault folder
4. Tell Cowork: `Go to https://github.com/rico/rico-second-brain-poc and run SETUP.md`

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
- `docs/faq.md` - common questions
- `docs/troubleshooting.md` - install issues
- `docs/connectors-approved.md` - Kipu-approved connector list

## License

Internal use only at Kipu Health and personal use of original author. No external distribution without permission. See `LICENSE`.
