# FAQ

## Why does the schedule require my machine to be on?

Cowork's scheduler runs in the desktop app process. It is not a true server-side cron. If your machine is off or asleep at the scheduled time, the schedule does not fire. We're tracking Anthropic's progress on a true cloud-side scheduler.

## Can I run this on a phone or tablet?

The vault is portable - point Obsidian Mobile at the same OneDrive folder and you can read/edit anywhere. But Cowork runs on desktop. Mobile access to the agent will land when Dispatch is available on Team / Enterprise plans.

## What if I leave Kipu?

Your work vault is **Kipu data** and stays with Kipu. It lives on Kipu's Microsoft 365 / OneDrive tenant, contains Kipu projects, meeting notes, decisions, and stakeholder context, and is governed by Kipu's data and IP policies. When you leave:

- Access to the OneDrive folder is revoked (standard offboarding).
- Access to Kipu's Cowork tenant — and to the org-shared `obsidian-vault` skill — is revoked.
- You may not copy, export, sync, or otherwise retain the vault contents on personal devices or accounts.

If you want this workflow for your **personal** life after leaving, you can stand up a fresh, empty vault on your own OneDrive / iCloud, run `SETUP.md` against it, and install the `obsidian-vault` skill from `releases/` in this repo (upload via claude.ai → Settings → Profile → Claude's skills). The scaffold and the skill are portable. Your Kipu vault contents are not.

## Can I customize this?

Yes. Anything in `Personalized` tier (CLAUDE.md, Context/context.md, Context/projects.md, Home.md) is yours to edit. Updates won't overwrite your changes - see UPGRADE.md.

## What if I don't like the three schedules?

Tell Cowork: "remove the [X] schedule" or "change my morning summary to 9am instead of 8am". Schedules are managed via the schedule skill.

## Why no PHI?

Until Anthropic signs a Business Associate Agreement (BAA) with Kipu, processing PHI through Claude is a HIPAA violation. The Compliance.md guardrail enforces this. Once the BAA is signed, the rule will be updated.

## Can I add my own connectors?

Do not connect personal accounts (personal Gmail, personal calendar, personal Slack, etc.) to your Kipu Cowork. Use only Kipu-approved connectors authenticated with your Kipu identity, routed through approved MCP servers with OAuth gating. See `docs/connectors-approved.md` for the current approved list and the request process for new ones.

## How do I add a custom skill?

Use the `skill-creator` skill in Cowork. It walks you through creating, testing, and packaging a new skill. Once created, you can keep it personal or share with your team / org via Cowork's per-skill share.

## How do I revert a bad update?

In v1.0.0 the update flow is not yet implemented, so there are no automatic `.scaffold-backup/` folders. If you want a snapshot before any manual change, copy `CLAUDE.md` and your `Context/` files to a side folder first. For restoring previous content, OneDrive version history (right-click the file → Version history → Restore) is your best option. Automatic backups land in a v1.x release.

## What if the obsidian-vault skill breaks something?

Toggle the skill off in Cowork: Settings → Skills → `obsidian-vault` → off. Start a new conversation. File an issue in the repo so it gets fixed for everyone.
