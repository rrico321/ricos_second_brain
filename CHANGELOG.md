# Changelog

## v1.0.2 - 2026-04-27 - Ship obsidian-vault.skill, drop placeholder

### Changed

- Added `releases/obsidian-vault.skill` (the actual fallback artifact for non-Kipu users)
- Removed `releases/obsidian-vault.plugin.PLACEHOLDER`
- Updated `SETUP.md`, `docs/troubleshooting.md`, `docs/how-it-works.md`, `docs/faq.md`, and `README.md` to reference `.skill` (claude.ai upload path) instead of `.plugin` (Claude Desktop path). Non-Kipu users install via claude.ai → Settings → Profile → Claude's skills.

## v1.0.1 - 2026-04-27 - Bootstrap fixes

Patch fixes flagged in initial audit.

### Fixed

- Added `scaffold/Templates/1on1 Prep Template.md` (was missing; SETUP.md Step 5 referenced it)
- `scaffold/Tasks/Tasks.md.template` now ships with only `### Personal` and `### Work`. SETUP.md Step 5 appends opt-in subheaders (Strategic Initiatives, Direct Reports, Stakeholder Comms, Decisions Pending) only if the user said yes
- `scaffold/CLAUDE.md.template` Manager line now uses `{{manager_name_or_none}}` placeholder; SETUP.md substitutes `(none)` if Q6 was skipped
- SETUP.md Step 4 now documents default substitutions for skipped/empty interview answers
- SETUP.md Step 6 project skeleton merged into a single fenced code block (was split into separate YAML and markdown blocks)
- SETUP.md Step 5 explicitly notes that `1on1 Prep Template.md` ships in scaffold and is already copied in Step 4 (no extra copy needed)

## v1.0.0 - 2026-04-27 - Initial release

First public version. Foundation for the Kipu Second Brain initiative.

### Added

- Vault scaffold (Daily Notes, Meeting Notes, Projects, People, Candidates, SOPs, Bugs & Issues, Templates, Context, Tasks, Settings)
- Personalized `CLAUDE.md` template with placeholders the interview fills in
- `Settings/Compliance.md` with HIPAA / no-PHI / BAA gap guardrails
- Four core schedules: Morning Summary (08:00 weekdays), Lint Noon (12:00 weekdays), Lint Evening (18:00 weekdays), Weekly Review (Friday 16:00)
- Templates: Daily Note, Meeting Note, Bug Report, Task
- Pre-filled `Context/glossary.md` with Kipu HL7 domain terms and general business terms
- Interview-driven optional folders: 1on1s, Decisions, Strategic Initiatives, Stakeholders
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
