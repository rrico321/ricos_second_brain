# Changelog

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
