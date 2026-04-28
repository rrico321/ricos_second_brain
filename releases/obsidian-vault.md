---
name: obsidian-vault
description: "Manage the user's Obsidian vault -- read, create, edit, and query notes using Dataview, Tasks, Templater, Calendar, and Excalidraw. Use this skill whenever the user asks to create a note, daily note, meeting note, project file, candidate file, task, diagram, Dataview query, or anything else involving their Obsidian vault. Also trigger when the user asks to search, update, archive, or summarize notes, add tasks, check open items, refresh memory/projects/index, or generate weekly/morning summaries. This skill knows the exact vault structure, naming conventions, task format, and how each plugin works. Always use this skill before touching any Obsidian file."
---
 
# Obsidian Vault Skill
 
You manage the user's personal Obsidian vault. This skill defines the authoritative structure, conventions, and workflows. Read it before touching any file in the vault.
 
## Mode Detection
 
If you are running in Cowork with a connected vault, follow the Vault Location section below for file access. If you are running in plain claude.ai with no file access, switch to advisory mode: produce the exact markdown content the user should paste into the appropriate vault file, name the destination path, and skip any read/write operations.
 
## Vault Location
 
The vault is the workspace folder the user has connected to this Cowork session. Do not hardcode a path - session mount paths change between sessions.
 
To resolve the vault root:
1. Use the connected workspace folder reported in `<env>` / file_handling_rules. The vault root is the top of that folder.
2. If no workspace is connected, call `request_cowork_directory` and ask the user to point at their Obsidian folder.
3. From bash, use the session-mount equivalent (e.g., `/sessions/<id>/mnt/Obsidian/`). Translate using the path-mapping table provided in the system context.
Confirm you are in the right folder by checking for `Home.md`, `index.md`, and `CLAUDE.md` at the root before writing anything.
 
## Vault Map
 
```
Obsidian/
├── CLAUDE.md             Routing rules. Always loaded by Claude. Do not edit casually.
├── README.md             Human-facing vault description.
├── Home.md               Navigation hub. Live Tasks query. Update when projects/SOPs change.
├── index.md              Full catalog of every page. Rebuild during health checks.
├── Context/
│   ├── context.md        User's role, team, stack, preferences. Read once at session start if needed.
│   ├── glossary.md       Domain terms, status labels, folder reference.
│   ├── memory.md         Append-only running log of session decisions and learnings.
│   └── projects.md       Quick-reference tracker for active projects.
├── Daily Notes/          YYYY-MM-DD.md
├── Meeting Notes/        YYYY-MM-DD - Title.md
├── Projects/             ProjectName.md (descriptive, no date prefix)
├── People/               FirstName LastName.md (or FirstName.md for close team)
├── Candidates/           FirstName LastName.md
├── Tasks/
│   ├── Tasks.md          Active tasks, organized under category subheaders.
│   └── Archive/Archive.md  Completed/cancelled tasks with ✅ date.
├── SOPs/                 SOP - Title.md
├── Bugs & Issues/        Free-form. Used for dashboards too.
└── Templates/            Templater source files. Read before creating new notes.
```
 
## Naming Conventions
 
- Daily notes: `YYYY-MM-DD.md`
- Meeting notes: `YYYY-MM-DD - Meeting Title.md`
- Projects: descriptive title, no date prefix (e.g., `API Migration Project.md`)
- People: `FirstName LastName.md` (preferred), or `FirstName.md` for close team members
- Candidates: `FirstName LastName.md`
- SOPs: `SOP - Title.md`
- Bugs: free-form descriptive title. The optional `BUG-YYYY-NNNN - Title.md` format is supported via the Bug Report Template but not strictly enforced.
## Templates Are Mandatory
 
Always read the matching template in `Templates/` before creating a new note of that type. Do not invent structure.
 
| Note type | Template file |
|-----------|---------------|
| Daily note | `Templates/Daily Note Template.md` |
| Meeting note | `Templates/Meeting Note Template.md` |
| Bug report | `Templates/Bug Report Template.md` |
| Task line | `Templates/Task Template.md` |
 
If a needed template does not exist (project, candidate, SOP, person), use the canonical examples already in the vault as the structural reference: read one existing file from that folder before creating a new one. This keeps frontmatter and section ordering consistent.
 
## Task Format (Tasks plugin emoji syntax)
 
Active tasks live in `Tasks/Tasks.md` under category subheaders (e.g., `### Project Alpha`, `### Operations`, `### Infrastructure`). Place new tasks under the most relevant subheader. Create a new subheader only when the existing categories clearly do not fit.
 
Status checkboxes:
- `- [ ]` not started
- `- [/]` in progress
- `- [x]` done
- `- [-]` cancelled
Line format:
```
- [ ] Task description ➕ 2026-04-13 📅 2026-04-20
- [ ] Task description ⏫ ➕ 2026-04-14 📅 2026-04-16
- [ ] Weekly report 🔁 every week on Monday ➕ 2026-04-14
```
 
| Emoji | Meaning | When to include |
|-------|---------|-----------------|
| ➕ | Created date | Always (today) |
| 📅 | Due date | Only if there is a hard deadline |
| ✅ | Done date | Added on completion or cancellation, before archiving |
| 🔁 | Recurrence | Only if the user says it recurs |
| 🔺 ⏫ 🔼 🔽 ⏬ | Priority (highest to lowest) | Only if the user states a priority |
 
Rules:
- Plain text descriptions. No bold, no italics, no leading emoji.
- Order on the line: description → priority (if any) → recurrence (if any) → ➕ date → 📅 date.
- Omit ➕/📅 emoji only if absent. Do not invent dates.
- The Tasks plugin parses these natively. Queries like `due before today`, `sort by urgency`, `sort by due date` work without extra metadata.
Full query syntax, sort/group options, and layout commands: see `references/tasks.md`.
 
## Frontmatter Conventions
 
Two formats are present in the vault. Use the YAML array form for any new file. Inline `#tag` form is acceptable when editing an existing file that already uses it.
 
Preferred (YAML array):
```yaml
---
tags: [project, ai, rag]
Status: In Progress
Owner: "[[{{preferred_name}}]]"
---
```
 
Status values in active use:
- Projects: `Active`, `In Progress`, `Completed`, `On Hold`
- Candidates: `Interviewed` (other expected lifecycle values: `Offer Extended`, `Hired`, `Passed`)
- Bugs: `Open` (other expected lifecycle values: `In Progress`, `Resolved`, `Closed`)
Always wrap wikilinked owners/people in quotes inside frontmatter: `Owner: "[[{{preferred_name}}]]"`.
 
## Wikilinks and People
 
Use `[[WikiLinks]]` for every person, project, and SOP reference in note bodies.
 
On first reference to a person in a session, run `ls People/` to confirm whether their file exists. If the user mentions someone new, either create a stub `People/` file or note the link as a missing page in your response.
 
## Wikilink Resolution
 
When a request hinges on a person, project, or SOP, resolve one level of links and synthesize across sources:
 
- Person query (e.g., "what is X working on?"): read `People/<Name>.md`, then scan `Meeting Notes/`, `Tasks/Tasks.md`, and `Projects/` for references.
- Project query: read the project file, then any meeting notes whose title or attendees suggest relevance, then the project's tasks subheader in `Tasks/Tasks.md`.
- Candidate query: read `Candidates/<Name>.md`, then `Tasks/Tasks.md` for related tasks.
- If a wikilink target file does not exist, surface it as a missing page in your response.
- Do not recursively follow every link. One level is usually enough.
## Tone and Style for Note Bodies
 
- Direct, no fluff.
- No emojis unless the user used one first or the format requires it (Tasks emoji metadata is exempt).
- No em dashes.
- Prose for summaries. Tables for structured data. Checkboxes for tasks.
- Headers and short paragraphs - keep notes scannable.
## Installed Plugins
 
Reference files are bundled with this skill at `references/` (sibling to this SKILL.md), not in the vault itself. Paths are relative to the skill directory.
 
| Plugin | Reference File | Use When |
|--------|---------------|----------|
| Dataview | `references/dataview.md` | Dashboards, queries over frontmatter, project rollups |
| Tasks | `references/tasks.md` | Task queries, filters, due-date logic, urgency sorting |
| Templater | `references/templater.md` | Creating or editing templates, date variables, prompts |
| Calendar | `references/calendar.md` | Daily/weekly note navigation, periodic notes |
| Excalidraw | `references/excalidraw.md` | Diagrams, architecture sketches |
 
Read the relevant reference file before writing any non-trivial query or template logic. If you can complete the task confidently from this SKILL.md alone, skip the reference.
 
---
 
## Common Operations
 
### Creating a Daily Note
1. Check whether `Daily Notes/YYYY-MM-DD.md` exists. If yes, append - do not overwrite.
2. If no, read `Templates/Daily Note Template.md` and use its structure (frontmatter `tags: #daily` and `date:`, then Focus Today / Notes / Tomorrow-Follow-up / Open Tasks query block).
3. Today's date comes from the env context, not from invention.
### Creating a Meeting Note
1. Read `Templates/Meeting Note Template.md`.
2. File path: `Meeting Notes/YYYY-MM-DD - Title.md`.
3. Populate frontmatter (`tags: #meeting`, `date:`, `attendees:`), Subject, Key Takeaways, and Owners table.
**Fathom transcripts.** See the dedicated "Processing a Fathom Transcript" workflow below.
 
### Processing a Fathom Transcript
1. Skim the transcript for `ACTION ITEM:` markers, intent statements ("I will", "we need to", "going to"), and any structured summary at the end. Do not read linearly.
2. Check whether a related Project note already has a synthesized summary. If yes, only fill gaps.
3. Extract decisions and action items into a new `Meeting Notes/YYYY-MM-DD - Title.md` (read template first).
4. For each action item with an identifiable owner, append a task to `Tasks/Tasks.md` under the appropriate subheader.
5. Cross-link to the related Project note.
### Adding a Task
1. Open `Tasks/Tasks.md`.
2. Find the right `### Subheader`. Create a new subheader only if no existing one fits.
3. Append: `- [ ] Description ➕ <today> 📅 <due if any>`. Add priority emoji only if the user stated a priority.
4. Update the bold `**Last Updated:** YYYY-MM-DD` stamp at the top of the file.
### Archiving Completed Tasks
1. For each `- [x]` (or `- [-]` cancelled) task in `Tasks/Tasks.md`, append `✅ <today>` if not already present.
2. Move the line to `Tasks/Archive/Archive.md` under `## Completed Tasks`.
3. Preserve the original ➕ and 📅 dates.
4. Update the bold `**Last Updated:** YYYY-MM-DD` stamp in `Tasks.md`.
### Creating a Project File
1. Read an existing project file for structural reference.
2. File: `Projects/<Project Name>.md`.
3. Frontmatter is required for index and dashboard queries to work:
   ```yaml
   ---
   tags: [project, <category>]
   Status: Active | In Progress | Completed | On Hold
   Owner: "[[{{preferred_name}}]]"
   ---
   ```
4. Body sections: Status, Owner, Stakeholders, Objective, Architecture or Approach (if technical), Open Questions, Next Steps or Timeline, Risks, Related links.
5. Use the user's stated details. Do not invent objectives or timelines. If something is unspecified, leave the section blank or with a placeholder and flag it in your response.
6. Add the project to `Home.md` under `## Active Projects` and to `index.md` under the Projects table.
### Creating a Candidate File
1. Read an existing candidate file for the canonical structure.
2. File: `Candidates/<First Last>.md`.
3. Frontmatter:
   ```yaml
   ---
   tags: [candidate, interview, <team-tag>]
   Status: Interviewed
   Position: <Role>
   Interview Date: YYYY-MM-DD
   Interviewer: "[[{{preferred_name}}]]"
   Recruiter: <Name (Source)>
   ---
   ```
4. Body sections: Background, Technical Skills, Interview Notes (subsections per question/topic), Expectations, Strengths, Concerns, Resume, Related.
5. Add the candidate to `Home.md` under `## Candidates` and to `index.md` under the Candidates table.
6. Cross-link to any related project or team notes.
### Creating a Person Stub
1. File: `People/<First Last>.md` or `People/<First>.md` for close team.
2. Minimal frontmatter (`tags: #person`, `role:`).
3. Body: Role, Recurring meetings (if any), Notes, Recent Context.
4. Add to `Home.md` Team list if internal.
5. Add to `index.md` People table.
### Creating an SOP
1. File: `SOPs/SOP - <Title>.md`.
2. Frontmatter `tags: [sop, <category>]`, `Owner: "[[{{preferred_name}}]]"`.
3. Body: Purpose, Scope, Trigger, Steps (numbered), Roles, References.
4. Add to `Home.md` SOPs list and `index.md` SOPs table.
### Morning Summary
Inputs: `Tasks/Tasks.md`, the most recent `Daily Notes/`, recent `Meeting Notes/`, all active `Projects/` files.
 
Today's date comes from `<env>`. Compute "overdue" and "due within 3 days" against that date.
 
Output exactly these four sections, in this order:
 
1. **Overdue** - tasks where 📅 < today. Each line: task description, days overdue, project context if obvious from the subheader.
2. **Due within 3 days** - tasks where today ≤ 📅 ≤ today+3. Each line: task, due date, blockers visible from project notes.
3. **No due date, created 5+ days ago** - tasks that may be stale or forgotten.
4. **Project status** - one line per active project: status and next milestone.
Empty-state rule: if a category has nothing, write `None.` Never silently skip and never fabricate. If a query returns no results, say so explicitly with the filter used and offer the closest available alternative (e.g., "No meeting notes from last week. Closest: 2026-04-02.").
 
Keep it scannable. No paragraphs.
 
### Weekly Review
Trigger: "weekly review", "Friday wrap", "what shipped this week".
 
Inputs: `Tasks/Tasks.md`, `Tasks/Archive/Archive.md`, all `Daily Notes/` from the past 7 days, all `Meeting Notes/` from the past 7 days, all active `Projects/` files, `Context/memory.md`.
 
Steps:
1. Archive completed tasks: move all `- [x]` and `- [-]` lines from `Tasks/Tasks.md` to `Tasks/Archive/Archive.md`, appending `✅ <today>` if not already present.
2. List tasks completed this week (from archive, filter by ✅ date within 7 days).
3. List new tasks added this week (filter by ➕ date within 7 days).
4. One-line status for each active project, noting any status changes this week.
5. Surface stale items: tasks with no due date created 10+ days ago, projects in `Active` status with no updates in 14+ days.
6. Append a memory.md entry summarizing the week: what shipped, key decisions, open risks.
Output format: six sections matching the steps above. Keep it scannable.
 
---
 
## Vault Maintenance Workflows
 
### Append to memory.md
Trigger: end of a substantive Cowork session, or when the user says "log this", "remember", or "save to memory".
 
1. Open `Context/memory.md`.
2. Insert a new entry directly under the `# Memory Log` header (newest at top).
3. Format:
   ```
   ## YYYY-MM-DD - Short Title
   - What happened
   - Decision made
   - Preference noted
   - Lesson learned
   ```
4. Keep entries tight. One bullet per discrete fact. No prose.
### Update projects.md
Trigger: project status change, new project, project archived.
 
1. Open `Context/projects.md`.
2. Update the relevant project's row. If a new project, add it. If completed/cancelled, move it to the appropriate section.
3. Keep this file as a quick-reference tracker, not a deep dive - one or two lines per project.
### Update Home.md
Trigger: new project, new SOP, new candidate, new dashboard, new template, team change.
 
1. Open `Home.md`.
2. Add or remove the link in the matching section (Active Projects, SOPs, Dashboards, Recent Meeting Notes, Team, Candidates, Templates).
3. Keep ordering: most recently active items first within each list.
4. Do not modify the `## Active Tasks` query block - it is a live Tasks query.
### Rebuild index.md
Trigger: the user asks for a vault health check, lint, "rebuild index", or after a batch of vault changes.
 
1. Scan the entire vault: every `.md` file outside `.obsidian/` and outside `Templates/` (templates listed in their own table).
2. For each file, derive a one-line summary from its title, frontmatter, and first paragraph.
3. Group into the existing index.md categories: Projects, People, Candidates, SOPs, Bugs & Issues, Tasks, Daily Notes, Meeting Notes, Context, Templates, Other.
4. Update `**Last rebuilt:**` and `**Total pages:**` at the top.
5. Run health checks and append to the `### Health Check` section:
   - **Orphan pages** - files with no inbound links from any other vault file. Use grep across all `.md` for `[[Filename]]` references.
   - **Missing pages** - wikilinks that point to files that do not exist. Grep all `[[...]]` patterns and check each target.
   - **Stale content** - daily notes more than 14 days old that are still the most recent, dashboards with snapshot dates more than 7 days old, projects in `Active` status with no updates in their file in 30+ days.
6. Report findings concisely. Do not delete anything without confirmation.
### Vault Lint (lighter than full rebuild)
Trigger: "check vault health", "any broken links", "what's stale".
 
Same checks as above, but report only - do not rewrite `index.md`.
 
---
 
## Empty-State and Honesty Rules
 
- If a query returns nothing, say so explicitly with the filter used. Never fabricate.
- If a wikilink target is missing, surface it as a missing page in your response.
- If the user asks about something not represented in the vault (e.g., a person who has no file), say so and offer to create a stub.
- If a template is missing or out of date, flag it - do not silently work around it.
