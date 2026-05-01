# Vault Workflows — What You Can Ask Cowork to Do

Quick reference for everything the `obsidian-vault` skill knows how to do. Use exact trigger phrases or anything similar in plain English — Cowork matches semantically, not literally.

If a workflow isn't listed here, the skill probably doesn't have a dedicated handler for it — but you can always ask in plain English ("create a folder for X", "search for notes mentioning Y") and Cowork will use its general file tools.

## Daily-driver workflows

| Workflow | Trigger phrases | What it does | When it runs |
|---|---|---|---|
| **Morning Summary** | "Run my morning summary", "Morning brief", "What's on my plate today" | 4-section briefing: Overdue tasks, Due within 3 days, Stale undated, Project status | Scheduled 8:00 weekdays + on-demand anytime |
| **Vault Tidy** | "Tidy my vault", "Run tidy", "Vault tidy" | Full housekeeping: archive completed tasks, rebuild `index.md`, sync `Context/projects.md`, update `Home.md` linked sections, append a Memory entry, surface orphans / missing wikilinks / stale projects / dangling tasks / Inbox count | Scheduled 12:00 + 18:00 weekdays + on-demand anytime |
| **Sort Inbox** | "Sort inbox", "Triage inbox", "Process inbox", "Clean my inbox" | Classifies each `Inbox/` item (Task, Meeting note, Project content, Person update, Drop), proposes destinations and filenames, moves on your approval. Never auto-classifies. | On-demand only |
| **Weekly Review** | "Weekly review", "Friday wrap", "What shipped this week" | End-of-week summary: completed tasks, new tasks, project status changes, stale items, plus a Memory.md entry summarizing the week | On-demand only |

## Adding content

| Workflow | Trigger phrases | What it does |
|---|---|---|
| **Add a Task** | "Add a task: ...", or describe a task in conversation ("I need to follow up on X by Friday") | Appends to `Tasks/Tasks.md` under the right `### Subheader` with proper emoji metadata (➕ created, 📅 due, priority if stated). Updates Last Updated stamp. |
| **Create Daily Note** | "Create today's daily note", or just open Obsidian — Templater can also auto-create | Self-routing template → `Daily Notes/YYYY-MM-DD.md`. Frontmatter, Focus Today, Notes, Tomorrow / Follow-up, live Open Tasks query block. |
| **Create Meeting Note** | "I had a meeting with X about Y, add it to my obsidian", or paste meeting notes | Self-routing template → `Meeting Notes/YYYY-MM-DD - Title.md`. Subject, Key Takeaways, Owners table, Related links. |
| **Process Fathom Transcript** | Paste a Fathom transcript, or "process this Fathom transcript" | Skims for action items and decisions, applies the Compliance read-first rule, scopes to your ownership only, files into `Meeting Notes/` + appends owner-tasks to `Tasks/Tasks.md` |
| **Create 1:1 Prep Note** | "Prep my 1:1 with X", "Draft a 1:1 with X" | Self-routing template → `1on1s/<Name>/YYYY-MM-DD - 1on1.md`. Wins, Blockers, Career, Decisions Needed, Agenda, Notes, Action Items. *(Only if `1on1s/` opt-in folder exists.)* |
| **Create Project File** | "Start a new project: X", "Create a project for X" | New file in `Projects/<Name>.md` with `tags`, `Status`, `Owner` frontmatter and body sections (Objective, Stakeholders, Next Steps, Risks, Related). Updates `Home.md` and `index.md`. |
| **Create Candidate File** | "I just interviewed X for the Y role", "Add a candidate file for X" | New file in `Candidates/<Name>.md` with hiring-specific frontmatter (Status, Position, Interview Date, Interviewer, Recruiter) and body sections. *(Only if `Candidates/` opt-in folder exists.)* |
| **Create Person Stub** | "Add X to my people list", "Create a person file for X" | Minimal `People/<Name>.md` — just enough frontmatter and structure to start linking from notes. |
| **Create SOP** | "Document SOP for X", "Create a runbook for X" | New file in `SOPs/SOP - <Title>.md` with Purpose, Scope, Trigger, Steps, Roles, References. |

## Maintenance / hygiene (Tidy auto-runs these — but you can trigger any individually)

| Workflow | Trigger phrases | What it does |
|---|---|---|
| **Append to Memory** | "Log this", "Remember that", "Save to memory" | New entry in `Context/Memory.md` under the `# Memory Log` header, newest at top. Date-stamped, tight bullets. |
| **Update projects.md** | "Update my project tracker", "Sync projects.md" | Reconciles `Context/projects.md` with current `Projects/` files — adds new, moves status changes, removes deleted. |
| **Update Home.md** | "Refresh Home.md", "Update my Home page" | Adds/removes links in Home.md's Active Projects, SOPs, Recent Meeting Notes, Team, Candidates, Templates sections to match current vault state. Never touches the live Tasks query block. |
| **Rebuild index.md** | "Rebuild the index", "Refresh the vault catalog", "Vault health check" | Full vault catalog rebuild with one-line summaries per file. Updates `Last rebuilt` and `Total pages`. Runs Tidy health checks and appends findings. |
| **Archive Completed Tasks** | "Archive my completed tasks" | Moves all `- [x]` and `- [-]` lines from `Tasks/Tasks.md` to `Archive.md` with `✅ <today>` stamp. Updates Last Updated. |

## Asking questions about the vault

These aren't formal workflows — Cowork uses its file tools to answer. Examples:

- "What is X working on?" — reads `People/X.md`, scans `Meeting Notes/`, `Tasks/Tasks.md`, and `Projects/` for references.
- "What's the status of project Y?" — reads `Projects/Y.md` and any related meeting notes.
- "What did we decide about Z?" — searches `Context/Memory.md` and recent meeting notes.
- "List my open tasks for project Y" — reads `Tasks/Tasks.md` and filters by subheader / wikilink.
- "What candidates are at offer-extended?" — scans `Candidates/` frontmatter for `Status: Offer Extended`.

## How to phrase requests

You don't need exact trigger phrases. The skill matches semantically. All of these work:

- "Give me my morning summary" / "What's on my plate today?" / "Run morning brief" → Morning Summary
- "Tidy" / "Clean up the vault" / "Run vault maintenance" → Vault Tidy
- "Process my inbox" / "What's in my inbox?" / "Sort what I've dropped" → Sort Inbox
- "Friday recap" / "Weekly summary" / "What did I ship this week?" → Weekly Review

If Cowork doesn't pick up the right workflow, name it explicitly: *"Run the Vault Tidy workflow."*

## Workflows that need opt-in folders

Some workflows depend on folders that are only created if you said "yes" to specific interview questions during `SETUP.md`:

| Workflow | Required folder | Interview question |
|---|---|---|
| Create 1:1 Prep Note | `1on1s/<Name>/` | Q7: "Do you manage people?" |
| Create Candidate File | `Candidates/` | Q11: "Do you participate in hiring?" |

If the folder doesn't exist, ask Cowork to create it: *"Create a 1on1s folder for Maria"* or *"Add a Candidates folder."* You don't need to re-run setup.

## Compliance always applies

Every workflow above runs the Compliance read-first rule before processing any external content (transcripts, connector data, pasted material). PHI is hard-refused until your org's BAA with the LLM provider is signed. See `COMPLIANCE.md` for the full rules.
