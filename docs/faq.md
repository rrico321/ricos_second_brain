# FAQ

## Why does the schedule require my machine to be on?

Cowork's scheduler runs in the desktop app process. It is not a true server-side cron. If your machine is off or asleep at the scheduled time, the schedule does not fire. We're tracking Anthropic's progress on a true cloud-side scheduler.

## Can I run this on a phone or tablet?

The vault is portable - point Obsidian Mobile at the same OneDrive folder and you can read/edit anywhere. But Cowork runs on desktop. Mobile access to the agent will land when Dispatch is available on Team / Enterprise plans.

## What if I leave Kipu?

Your vault belongs to you. The OneDrive folder syncs to your account. The CLAUDE.md and Context files transfer with the vault. The obsidian-vault skill is shared via Kipu's Cowork tenant - you lose access to it when you leave, but the `.skill` file in `releases/` in this repo is a fallback (upload via claude.ai → Settings → Profile → Claude's skills).

## Can I customize this?

Yes. Anything in `Personalized` tier (CLAUDE.md, Context/context.md, Context/projects.md, Home.md) is yours to edit. Updates won't overwrite your changes - see UPGRADE.md.

## What if I don't like the four schedules?

Tell Cowork: "remove the [X] schedule" or "change my morning summary to 9am instead of 8am". Schedules are managed via the schedule skill.

## Why no PHI?

Until Anthropic signs a Business Associate Agreement (BAA) with Kipu, processing PHI through Claude is a HIPAA violation. The Compliance.md guardrail enforces this. Once the BAA is signed, the rule will be updated.

## Can I add my own connectors?

For personal data: yes, your personal connectors (Gmail, calendar, etc.) work. For Kipu data: route through approved MCP servers with OAuth gating. See docs/connectors-approved.md.

## How do I add a custom skill?

Use the `skill-creator` skill in Cowork. It walks you through creating, testing, and packaging a new skill. Once created, you can keep it personal or share with your team / org via Cowork's per-skill share.

## How do I revert a bad update?

Updates create `.scaffold-backup/<old-version>/` folders in your vault. Copy files back from there to revert. There is no formal rollback - this is markdown, not code.

## What if the obsidian-vault skill breaks something?

Tell Cowork: "stop using the obsidian-vault skill for this session" and try a different approach. File an issue in the repo so it can be fixed for everyone.
