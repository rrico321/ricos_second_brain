# UPGRADE.md — Planned Update Model

> ⚠️ **Status: not implemented in v1.0.x.** This document describes the **planned** automated update flow targeted for a v1.x release. None of the automation described below exists today. For the v1.0.x manual workflow, see "How to update today" at the bottom of this file.

This repo will evolve over time. Your vault will be a mix of repo-derived files (the scaffold) and your personal content. Updates will touch the scaffold; they will never touch your content.

---

## Planned three-tier file model

When the update flow ships, every file in your vault will fall into one of three tiers:

| Tier | Files | Planned update behaviour |
|------|-------|-----------------|
| **Core scaffold** | `Context/Compliance.md`, `Templates/*`, schedule definitions | Will be replaced on update. Old version backed up to `.scaffold-backup/<old-version>/` automatically. |
| **Personalized** | `CLAUDE.md`, `Context/context.md`, `Context/projects.md`, `Home.md` | Never auto-replaced. New template additions surfaced as a diff; you decide what to merge. |
| **User content** | `Daily Notes/`, `Meeting Notes/`, `Projects/`, `Tasks/`, `Candidates/`, `People/`, `Issues/`, `SOPs/`, `Inbox/`, `1on1s/`, `Stakeholders/`, `Strategic Initiatives/`, `Context/Memory.md` | Never touched. Ever. |

This three-tier guarantee — especially the "never touched" promise on user content — is the design contract of the update model.

## Planned versioning model

Semver-style:

- **Patch (`1.0.x`)** — bug fixes only. Will be auto-applicable.
- **Minor (`1.x.0`)** — new templates, new schedules, refined skill prompts. Opt-in via the update flow.
- **Major (`x.0.0`)** — breaking changes. Opt-in with explicit migration notes in `CHANGELOG.md`.

Your installed version lives in `Context/.scaffold-version.yaml` in your vault. That file already exists and tracks your installed version (currently `1.0.4`); it will be the input to the planned diff flow.

## Planned `Check for second-brain updates` flow

When implemented, the user will say to Cowork: **`Check for second-brain updates`**, and Cowork will:

1. Read the latest `CHANGELOG.md` from the repo.
2. Compare against the installed version in `Context/.scaffold-version.yaml`.
3. Walk the user through each change since their installed version.
4. Back up Core scaffold files to `.scaffold-backup/<old-version>/` before replacing them.
5. Show diffs for Personalized files and ask before merging anything.
6. Update `Context/.scaffold-version.yaml` when done.

If a user manually edited a Core scaffold file (e.g., a Template), the planned flow will detect the diff and ask before overwriting. They can keep their custom version, in which case they stay on the old scaffold version for that file.

## Planned rollback story

The planned model has **no formal rollback command.** The `.scaffold-backup/<old-version>/` folder will preserve prior versions of replaced Core scaffold files; rollback will be a manual copy-back from that folder.

## Skill updates (always out of band)

The `obsidian-vault` skill itself is NOT and will NOT be updated through this repo's update flow. It is shared via Cowork's per-skill share toggle. When the skill owner publishes a change, it propagates to everyone with the share instantly. The `.skill` artifact in `releases/` is the fallback for non-Kipu users and is updated manually when the skill ships meaningful changes. Your `Context/.scaffold-version.yaml` does not track skill version.

PR-driven skill source updates (a `skills/` source tree in this repo with a build step that produces the `.skill` artifact) are out of scope for v1.0 and a v1.x consideration if contributor demand emerges.

---

## How to update today (v1.0.x)

Until the automated flow ships, updates are manual:

1. **Watch `CHANGELOG.md`** in the repo for changes that affect you.
2. **Apply notable changes by hand** to your vault — copy updated `Templates/*`, edit `Context/Compliance.md` if it changed, adjust schedule trigger phrases if renamed, etc.
3. **For rollback or recovery:** use OneDrive version history (right-click file → Version history → Restore). This works on every file in the vault.
4. **Bump `Context/.scaffold-version.yaml`** by hand if you applied a meaningful set of changes, so future you knows where you are.

For a fresh install or a from-scratch reset, run `SETUP.md` against a new empty vault and copy your `Daily Notes/`, `Meeting Notes/`, `Projects/`, `Tasks/`, etc. across by hand.
