# UPGRADE.md - How Updates Work

This repo evolves over time. Your vault is a mix of repo-derived files (the scaffold) and your personal content. Updates touch the scaffold and never touch your content.

## Three-tier file model

| Tier | Files | Update behavior |
|------|-------|-----------------|
| **Core scaffold** | `Context/Compliance.md`, `Templates/*`, schedule definitions | Replaced on update. Old versions backed up to `.scaffold-backup/<old-version>/` automatically. |
| **Personalized** | `CLAUDE.md`, `Context/context.md`, `Context/projects.md`, `Home.md` | Never auto-replaced. New template additions surfaced as a diff. You decide what to merge. |
| **User content** | `Daily Notes/`, `Meeting Notes/`, `Projects/`, `Tasks/`, `Candidates/`, `People/`, `Issues/`, `SOPs/`, `1on1s/`, `Stakeholders/`, `Strategic Initiatives/`, `Context/Memory.md` | Never touched. Ever. |

## Versioning

Semver-style:

- Patch (`1.0.x`): bug fixes only. Auto-applicable.
- Minor (`1.x.0`): new templates, new schedules, refined skill prompts. Opt-in via update flow.
- Major (`x.0.0`): breaking changes. Opt-in with explicit migration notes in `CHANGELOG.md`.

Your installed version lives in `Context/.scaffold-version.yaml` in your vault.

## How to check for updates

In Cowork, say: **`Check for second-brain updates`**

Cowork will:

1. Read the latest `CHANGELOG.md` from the repo
2. Compare against your installed version
3. Walk you through each change
4. Back up Core scaffold files to `.scaffold-backup/<old-version>/` before replacing
5. Show diffs for Personalized files and ask before merging anything
6. Update `Context/.scaffold-version.yaml` when done

## What if I customized a Core scaffold file?

If you manually edited a Core scaffold file (e.g., a Template), Cowork detects the diff and asks before overwriting. You can keep your custom version, in which case you stay on the old scaffold version for that file.

## Rollback

There is no formal rollback. The `.scaffold-backup/` folder preserves prior versions of replaced files. To roll back, copy them back manually.

## Skill updates

The `obsidian-vault` skill itself is NOT updated through this repo. It is shared via Cowork's per-skill share toggle. When the skill owner publishes a change, it propagates to everyone instantly. Your `Context/.scaffold-version.yaml` does not track skill version.
