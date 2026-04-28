# Vault Anatomy

A tour of every folder and file in your vault — what it is, when it's used, and who reads it (you, Cowork, or both). Use this as orientation after `SETUP.md` finishes, or as a refresher when the vault starts to feel like too much.

## Root files (auto-loaded by Cowork)

| File | What it is | How it's used | Purpose |
|---|---|---|---|
| `CLAUDE.md` | Routing manifest. Lists who you are, what to read first, and which skill handles what kind of request. | Cowork reads it on every session start. You rarely edit. | Single source of truth for agent behavior in this vault. Anything in here overrides default Cowork behavior. |
| `Home.md` | Your manual dashboard. Live Tasks query, active projects, recent meeting notes, team links. | Open in Obsidian when you want a human view of "what's going on." | Human-facing nav hub. Cowork doesn't depend on it. |
| `index.md` | Catalog of every page in the vault with one-line summaries. | Cowork reads it before drilling into specific files. The lint workflows refresh it. | Lets Cowork orient without scanning the whole vault. |

## Daily-flow folders (you write here all the time)

| Folder | Naming | When | Purpose |
|---|---|---|---|
| `Daily Notes/` | `YYYY-MM-DD.md` | One per workday. Use the `Daily Note Template`. | Journal + scratchpad. Focus, free notes, tomorrow / follow-ups, live open-tasks query. |
| `Meeting Notes/` | `YYYY-MM-DD - Title.md` | One per meeting. Auto-created when you say "I had a meeting with X" or paste a transcript. | Permanent record: subject, key takeaways, owners table, links back to projects/people. |
| `Tasks/` | `Tasks.md` (active), `Archive/Archive.md` (done) | Add tasks anywhere in conversation. Lint Evening archives `[x]` and `[-]` lines. | Single source of truth for everything you owe or are tracking. Powered by the Tasks plugin so queries like "due before today, sort by urgency" just work. |

## Context / reference (read by Cowork on demand)

| Folder | What's in it | Purpose |
|---|---|---|
| `Context/Compliance.md` | HIPAA / PHI / BAA hard-rules. | First file Cowork reads. Hard-blocks any PHI work until BAA is signed. |
| `Context/context.md` | Your role, team, comm style, output prefs. | Personalization. Cowork reads it to know how to talk to you. |
| `Context/Glossary.md` | HL7, LOINC, ASAM levels, Kipu product line, status labels, vault folder reference. | Domain dictionary. Avoids you having to re-explain "PHP" or "VOB" each session. |
| `Context/Memory.md` | Append-only running log of decisions, preferences, learnings. | Long-memory across sessions. Newest entry at top. |
| `Context/projects.md` | Quick-reference table: project, status, owner, next milestone. | Project rollup. Updated when projects change state. |
| `Context/.scaffold-version.yaml` | System file. Tracks installed scaffold version + your interview answers. | Used by the planned update flow (see Note below). Don't edit by hand. |

## Knowledge folders (you populate over time)

| Folder | Naming convention | Use |
|---|---|---|
| `Projects/` | `<ProjectName>.md`, no date prefix | One file per active initiative. Frontmatter has `tags`, `Status`, `Owner`. Body: Objective, Stakeholders, Next Steps, Risks, Related. |
| `People/` | `FirstName LastName.md` (or just `FirstName.md` for close team) | Team members, peers, collaborators. One file per person. |
| `SOPs/` | `SOP - <Title>.md` | Standard operating procedures. Body: Purpose, Scope, Trigger, Steps, Roles, References. |
| `Issues/` | Free-form, or `BUG-YYYY-NNNN - Title.md` if you want | Bug reports, ops issues, ad-hoc dashboards (e.g., interface health snapshot). |
| `Templates/` | Existing templates ship from scaffold | Templater source files. Daily Note / Meeting Note / Bug Report / Task / 1on1 Prep templates all live here. Don't edit unless you're redesigning the note structure. |

## Opt-in folders (created only if you said yes during setup)

| Folder | Triggered by | Purpose |
|---|---|---|
| `1on1s/` | Q7 ("Do you manage people?") with at least one direct-report name | One subfolder per direct report. Use the `1on1 Prep Template` to draft 1:1 agendas. Notes from each 1:1 land here. |
| `Strategic Initiatives/` | Q9 ("Do you track strategic initiatives or OKRs separately?") yes | Top-level themes that span quarters and multiple projects. Different scope from `Projects/`, which is execution-level. |
| `Stakeholders/` | Q10 ("Do you have external stakeholders?") yes | Board, investors, key customers. One file per stakeholder. |
| `Candidates/` | Q11 ("Do you participate in hiring?") yes | One file per candidate you're interviewing. Frontmatter: `Status`, `Position`, `Interview Date`, `Interviewer`, `Recruiter`. Lifecycle: Interviewed → Offer Extended → Hired/Passed. On hire, create a `People/` file and leave the `Candidates/` file alone as history. |

If you said "no" to any of these during the interview, the matching folder simply doesn't exist in your vault. You can ask Cowork to add it later if your role changes.

## How it all flows in a typical week

1. **08:00 weekday** — `Morning Summary` schedule fires. Cowork reads `CLAUDE.md` → loads the `obsidian-vault` skill → reads `Tasks/Tasks.md`, the most recent `Daily Notes/`, recent `Meeting Notes/`, and active `Projects/`. Output: 4 sections (Overdue, Due in 3 days, Stale undated, Project status).
2. **Throughout the day** — meetings produce `Meeting Notes/<date> - Title.md` with action items pushed into `Tasks/Tasks.md` under `### Work`. Decisions worth keeping go to `Context/Memory.md`.
3. **12:00 weekday** — `Lint Noon` runs read-only health check: orphan pages, broken wikilinks, stale daily notes, `Active` projects with no recent updates.
4. **18:00 weekday** — `Lint Evening` runs the same lint plus archives any `- [x]` / `- [-]` task lines from `Tasks.md` to `Archive.md` with a `✅ <today>` stamp.

## Three-tier file model (worth knowing)

| Tier | Files | Update behavior (planned, see Note) |
|---|---|---|
| Core scaffold | `Context/Compliance.md`, `Templates/*`, schedule definitions | Will be replaced on update. Old version backed up to `.scaffold-backup/<old-version>/`. |
| Personalized | `CLAUDE.md`, `Context/context.md`, `Context/projects.md`, `Home.md` | Will never auto-replace. Diff is shown, you decide what to merge. |
| User content | Everything in `Daily Notes/`, `Meeting Notes/`, `Projects/`, `Tasks/`, `People/`, `Candidates/`, `Issues/`, `SOPs/`, `1on1s/`, `Strategic Initiatives/`, `Stakeholders/`, `Context/Memory.md` | Never touched on update. Ever. |

> **Note on updates:** The `cowork check for second-brain updates` flow and the automatic `.scaffold-backup/` mechanism are documented in `UPGRADE.md` but **not yet implemented in v1.0.x**. For now, if you want to roll back a manual change, use OneDrive version history (right-click file → Version history). The auto-update flow lands in a v1.x release.
