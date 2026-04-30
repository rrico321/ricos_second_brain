# SETUP.md - Bootstrap a Personalized Second Brain

This file is read by Claude Cowork. If you are a human reading this, you don't need to do anything except tell Cowork: `Go to this repo and run SETUP.md`.

## Cowork: read this section in full before starting

You are bootstrapping a personalized Obsidian vault for the user. Walk through every step in order. Ask questions in plain English. Use your file tools (Read, Write, Edit) to operate on files inside the user's vault folder. Use `mcp__scheduled-tasks__create_scheduled_task` to create schedules.

Never:
- Run shell commands
- Touch files outside the user's vault folder
- Skip the interview
- Assume answers if the user does not respond
- **Batch interview questions.** Do NOT ask multiple questions in one message, do NOT use AskUserQuestion to bundle several questions, and do NOT pre-fill answers from any user profile or memory. The interview must be strictly sequential: one question, wait for the answer, next question.

Always:
- Confirm before destructive operations
- Use forward slashes in paths the user sees
- Translate paths per-OS when actually writing files
- Ask interview questions one at a time, in plain text, in the order listed in Step 3

The user is non-technical. Prefer plain English over jargon.

---

## Step 1: Confirm vault location

By the time SETUP.md is running, the user has already pointed Cowork at the folder where they want the vault built. Don't ask for a path — Cowork already knows its own working directory. The job here is to confirm, not to gather.

1. Identify your current working directory (the folder Cowork was pointed at when this session opened).
2. Tell the user, plainly:

   > "I'm about to build your second-brain vault in **`<folder name>`** (full path: `<absolute path>`). Everything will be written here. Sound right? (yes / no)"

   Use the actual folder name and absolute path — don't make the user type either.

3. If the user says **yes**, set the working directory as `<VAULT_ROOT>` and continue to Step 2.

4. If the user says **no**, do NOT prompt them for a different path. Tell them:

   > "No problem. Close this Cowork session, point Cowork at the folder you actually want the vault in, then re-run SETUP.md from there. The vault always builds in whatever folder Cowork is opened on."

   Then stop the script.

5. **OneDrive policy check (Kipu employees):** Before continuing, check whether the absolute path contains the substring `OneDrive` (case-insensitive). If it does NOT, warn the user:

   > "Heads-up: this folder isn't on Microsoft 365 / OneDrive. Per Kipu policy, company vaults must live on OneDrive. Do you want to abort and re-point Cowork at a OneDrive folder, or proceed with a documented override? (abort / proceed)"

   If they say **abort**, stop the script with the same "close Cowork, re-point at OneDrive folder, re-run SETUP.md" instruction.
   If they say **proceed**, continue and note the override for Step 10's report.

---

## Step 2: Detect existing setup

Check whether any of these exist in `<VAULT_ROOT>`:
- `CLAUDE.md`
- `Home.md`
- `index.md`
- `Context/.scaffold-version.yaml`

If any exist:
- Ask the user: **An existing scaffold was detected. v1.0 only supports fresh install. Continuing will overwrite scaffold files but preserve your content (Daily Notes, Meeting Notes, Projects, Tasks, etc.). Continue?**
- If no, abort cleanly.

---

## Step 3: Run the interview

Ask each question one at a time, in plain text, in the order listed below. Wait for the user's answer before moving to the next. Do not batch, do not pre-fill, do not use structured pickers.

1. **What is your full name?** (used in CLAUDE.md and Context)
2. **What is your preferred name?** (what Cowork should call you)
3. **What is your email address?**
4. **What is your job title?**
5. **What department do you work in?**
6. **Who is your direct manager?** (reply "none" if you do not have one)
7. **Do you manage people? If yes, list their first names separated by commas (e.g., "Maria, Jamal, Priya"). If not, reply "no".**
   *If yes:* I'll create a `1on1s/` folder with a subfolder per name, and add a `### Direct Reports / 1:1 follow-ups` subheader to your task list. *If no:* neither is created.
8. **Top three current projects or initiatives?** (free text, comma-separated — reply "skip" if you don't want to list any right now; you can add projects later by telling Cowork)
   *Effect:* I'll pre-create a `Projects/<Project Name>.md` file for each one with a starter template, and link them in `Home.md` and `index.md`.
9. **Do you track strategic initiatives or OKRs separately from project work?** (yes / no)
   *If yes:* I'll create a `Strategic Initiatives/` folder and add a `### Strategic Initiatives` subheader to your task list. *If no:* neither is created.
10. **Do you have external stakeholders to track?** (board, investors, key customers — yes / no)
    *If yes:* I'll create a `Stakeholders/` folder and add a `### Stakeholder Comms` subheader to your task list. *If no:* neither is created.
11. **Do you participate in hiring?** (interview candidates for open roles — yes / no)
    *If yes:* I'll create a `Candidates/` folder where you can drop one file per candidate you're interviewing. *If no:* the folder isn't created — you can ask me to add it later if your role changes.
12. **What communication style do you prefer from Cowork?** (reply with the number)
    1. Direct and concise (default)
    2. Conversational
    3. Detailed with explanations
13. **Any output preferences I should know about?** (free text, e.g., "no em dashes", "Spanish for family-related notes", "always include a TL;DR" — or reply "none")

Save all answers as `{{placeholder_name}}` values for the next steps.

---

## Step 4: Copy the base scaffold

For each file under `scaffold/` in this repo, copy it to `<VAULT_ROOT>` preserving the relative path.

For files ending in `.template`:
- Strip the `.template` extension
- Replace every `{{placeholder}}` with the corresponding interview answer
- Write the result to the destination

For `.gitkeep` files:
- Skip them. Just create the empty parent folder.

For non-template files (e.g., `Templates/Daily Note Template.md`):
- Copy verbatim.

### Default substitutions for skipped or empty answers

If the user skipped or left an answer blank, substitute these defaults before writing:

| Placeholder | Default if empty |
|-------------|------------------|
| `{{manager_name_or_none}}` | `(none)` |
| `{{output_preferences}}` | `(none specified)` |
| `{{communication_style}}` | `Direct and concise` |
| `{{project_1}}`, `{{project_2}}`, `{{project_3}}` | omit the project entirely (don't render an empty link) |
| `{{direct_reports_list}}` | `[]` |
| Any boolean placeholder (strategic_initiatives_enabled, etc.) | `false` |

Result: a fully populated vault with personalized `CLAUDE.md`, `Home.md`, `index.md`, `Context/context.md`, `Context/projects.md`, `Context/Compliance.md`, `Context/.scaffold-version.yaml`, and `Tasks/Tasks.md`.

---

## Step 5: Apply interview-driven additions

`Tasks/Tasks.md` ships with one base subheader: `### Work`. Add subheaders below for each opt-in the user selected. Do not add a subheader if the user said no.

If the user manages people (Q7 reply is not "no"):
- Create `<VAULT_ROOT>/1on1s/` folder
- For each first name in the Q7 reply, create `<VAULT_ROOT>/1on1s/<Name>/` subfolder with a `.gitkeep` (empty)
- Append `### Direct Reports / 1:1 follow-ups` to `Tasks/Tasks.md` under `## Active Tasks`
- The `1on1 Prep Template.md` is already shipped in `scaffold/Templates/` and copied to the user's `Templates/` folder in Step 4. No additional copy needed.

If the user tracks strategic initiatives (Q9 yes):
- Create `<VAULT_ROOT>/Strategic Initiatives/` folder with `.gitkeep`
- Append `### Strategic Initiatives` to `Tasks/Tasks.md` under `## Active Tasks`

If the user has external stakeholders (Q10 yes):
- Create `<VAULT_ROOT>/Stakeholders/` folder with `.gitkeep`
- Append `### Stakeholder Comms` to `Tasks/Tasks.md` under `## Active Tasks`

If the user participates in hiring (Q11 yes):
- Create `<VAULT_ROOT>/Candidates/` folder with `.gitkeep`

After all opt-in additions, remove the HTML comment block from `Tasks/Tasks.md` (the one starting with `<!-- Additional subheaders are added by SETUP.md`). It is no longer needed.

---

## Step 6: Pre-populate Projects

For each project name from Q8:
- Create `<VAULT_ROOT>/Projects/<Project Name>.md` with this exact content (single file, frontmatter + body):

````markdown
---
tags: [project]
Status: Active
Owner: "[[{{preferred_name}}]]"
---

# {{Project Name}}

**Status:** Active
**Owner:** [[{{preferred_name}}]]

## Objective

(fill in)

## Stakeholders

## Next Steps

## Risks

## Related
````

Update `Home.md` and `index.md` with these projects (add to Active Projects section in Home.md, add a row to the Projects table in index.md).

If the user replied "skip" to Q8, skip Step 6 entirely — do not create any project files, and leave the Active Projects section in `Home.md` and the Projects table in `index.md` empty (no rows).

If a project name slot is empty (user provided fewer than 3), skip that slot. Do not create empty project files.

---

## Step 7: Create the three base schedules

Use `mcp__scheduled-tasks__create_scheduled_task` for each. Read the schedule definition from `schedules/<name>.md` in this repo to get the trigger phrase, cron, and behavior.

| Name | Cron | Trigger phrase |
|------|------|----------------|
| Morning Summary | `0 8 * * 1-5` | "Run my morning summary" |
| Vault Tidy (Noon) | `0 12 * * 1-5` | "Tidy my vault" |
| Vault Tidy (Evening) | `0 18 * * 1-5` | "Tidy my vault and archive completed tasks" |

If the user's machine is unlikely to be on at 8am, suggest 9am as an alternative. Note that schedules require the user's machine to be on (Cowork's scheduler is not a true cron).

---

## Step 8: Verify the obsidian-vault skill

Check whether the `obsidian-vault` skill is enabled in the user's Cowork.

If yes: proceed.

If no:
- For Kipu employees: tell the user "Open Settings -> Skills in Cowork. The `obsidian-vault` skill should be in your Shared section. Toggle it on. Then say 'continue setup' here."
- For non-Kipu: tell the user "Download `releases/obsidian-vault.skill` from this repo, then go to claude.ai → Settings → Profile → Claude's skills and upload it. Then say 'continue setup' here."

---

## Step 9: Smoke test

- Add a sample task to `Tasks/Tasks.md` under any subheader: `- [ ] Setup smoke test (delete me) ➕ <today>`
- Invoke the morning summary workflow against the new vault
- Confirm the agent reads `CLAUDE.md`, finds `obsidian-vault` skill, follows `Tasks/Tasks.md`, and produces the four-section output
- Remove the sample task
- Update `Tasks/Tasks.md` `**Last Updated:**` stamp to today

---

## Step 10: Report what was done

Tell the user, concisely:

- Vault location confirmed
- N folders created (list any optional ones added)
- M files written (CLAUDE.md, Home.md, index.md, Context/*, Templates/*, Tasks/Tasks.md)
- 3 schedules registered
- obsidian-vault skill verified
- Smoke test passed

Then suggest three things to try in the next 24 hours:
1. Add a meeting note (just say "I had a meeting with X about Y, add it to my obsidian")
2. Tomorrow morning, watch the morning summary fire
3. Add tasks naturally as they come up in conversation

End with: "The automated update flow is not implemented in v1.0.x. To pull future repo changes manually, watch `CHANGELOG.md` in the repo and apply notable items by hand. The `cowork check for second-brain updates` command lands in a v1.x release."
