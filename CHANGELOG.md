# Changelog

## v1.0.4 - 2026-04-28 - Inbox folder, rename Lint to Tidy

### Added

- New `scaffold/Inbox/` folder. Capture-first dumping ground for content that doesn't have an obvious home (voice transcripts, half-formed ideas, links, screenshots).
- New on-demand workflow trigger: `sort inbox`. Cowork classifies Inbox items, proposes destinations, moves on user approval.
- FAQ entry: "What goes in Inbox/?"

### Changed

- **Renamed "Lint" to "Tidy" everywhere.** Audience-friendly term. "Lint" is engineering jargon; "Tidy" describes the actual behavior.
- `schedules/lint-noon.md` → `schedules/tidy-noon.md`. Schedule name `Vault Lint (Noon)` → `Vault Tidy (Noon)`. Trigger phrase `Run vault lint` → `Tidy my vault`.
- `schedules/lint-evening.md` → `schedules/tidy-evening.md`. Schedule name `Vault Lint (Evening)` → `Vault Tidy (Evening)`. Trigger phrase `Run vault lint and archive completed tasks` → `Tidy my vault and archive completed tasks`.
- Both Tidy schedules now also count items in `Inbox/` and flag if any are waiting (read-only - they don't auto-sort).
- Updated `SETUP.md` Step 7 schedule table with new names and trigger phrases.
- Updated `docs/how-it-works.md`, `docs/vault-anatomy.md`, `docs/faq.md`, `README.md`, `scaffold/README.md` to reference Tidy instead of Lint.
- Updated `scaffold/index.md.template` with `## Inbox (0)` section and corrected the maintenance note from `vault-lint` to `Vault Tidy`.

### Why

"Lint" came from engineering culture (linting code). The audience for this scaffold is non-technical leaders. "Tidy" tells them what the workflow actually does (light cleanup, surface what's off, archive what's done) without the engineering pedigree. The Inbox folder closes a real gap - users had nowhere to drop unstructured captures, so everything had to be filed in the moment.

## v1.0.2 - 2026-04-27 - Ship obsidian-vault.skill, drop placeholder

### Changed

- Added `releases/obsidian-vault.skill` (the actual fallback artifact for non-Kipu users)
- Removed `releases/obsidian-vault.plugin.PLACEHOLDER`
- Updated `SETUP.md`, `docs/troubleshooting.md`, `docs/how-it-works.md`, `docs/faq.md`, and `README.md` to reference `.skill` (claude.ai upload path) instead of `.plugin` (Claude Desktop path). Non-Kipu users install via claude.ai → Settings → Profile → Claude's skills.

## v1.0.1 - 2026-04-27 - Bootstrap fixes

Patch fixes flagged in initial audit.

### Fixed

- Added `scaffold/Templates/1on1 Prep Template.md` (was missing; SETUP.md Step 5 referenced it)
- `scaffold/Tasks/Tasks.md.template` now ships with only `### Work`. SETUP.md Step 5 appends opt-in subheaders (Strategic Initiatives, Direct Reports, Stakeholder Comms) only if the user said yes
- `scaffold/CLAUDE.md.template` Manager line now uses `{{manager_name_or_none}}` placeholder; SETUP.md substitutes `(none)` if Q6 was skipped
- SETUP.md Step 4 now documents default substitutions for skipped/empty interview answers
- SETUP.md Step 6 project skeleton merged into a single fenced code block (was split into separate YAML and markdown blocks)
- SETUP.md Step 5 explicitly notes that `1on1 Prep Template.md` ships in scaffold and is already copied in Step 4 (no extra copy needed)

## v1.0.0 - 2026-04-27 - Initial release

First public version. Foundation for the Kipu Second Brain initiative.

### Added

- Vault scaffold (Daily Notes, Meeting Notes, Projects, People, SOPs, Issues, Templates, Context, Tasks)
- Personalized `CLAUDE.md` template with placeholders the interview fills in
- `Context/Compliance.md` with HIPAA / no-PHI / BAA gap guardrails
- Three core schedules: Morning Summary (08:00 weekdays), Lint Noon (12:00 weekdays), Lint Evening (18:00 weekdays)
- Templates: Daily Note, Meeting Note, Bug Report, Task
- Pre-filled `Context/Glossary.md` with Kipu HL7 domain terms and general business terms
- Interview-driven optional folders: 1on1s, Strategic Initiatives, Stakeholders, Candidates
- `SETUP.md` bootstrap script Cowork reads and executes
- `UPGRADE.md` documenting the three-tier update model
- `docs/` folder: how-it-works, faq, troubleshooting, connectors-approved
- `releases/obsidian-vault.plugin.PLACEHOLDER` for non-Kipu fallback install

### Known gaps

- Skill source is not version-controlled in this repo. The `obsidian-vault` skill lives in Cowork and is shared org-wide. PR-driven skill updates are a v1.x followup.
- Update flow (`cowork check for second-brain updates`) is documented in `UPGRADE.md` but the corresponding skill workflow is not yet implemented in v1.0.0.
- Role packs (executive-leader, people-manager) are deferred. The interview drives all role-specific behavior in v1.0.
- Live Artifacts as vault dashboard layer not yet integrated.
- Dispatch (mobile capture channel) not yet available on Team / Enterprise plans.

### Migration notes

n/a (initial release).
