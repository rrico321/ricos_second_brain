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

Ask the user: **What is the absolute path to your Obsidian vault folder?**

Mac example: `/Users/<name>/Library/CloudStorage/OneDrive-KipuHealth/Obsidian`
Windows example: `C:/Users/<name>/OneDrive - Kipu Health/Obsidian`

Verify the folder exists. If not, ask the user to create it and re-confirm.

If the user is on a Kipu Health email and the path does NOT contain `OneDrive`, warn them: per Kipu policy, company vaults must live on Microsoft 365 / OneDrive. Offer to abort or proceed with a documented override.

Set the verified path as `<VAULT_ROOT>` for the rest of this script.

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
8. **Top three current projects or initiatives?** (free text, comma-separated)
9. **Do you track strategic initiatives or OKRs separately from project work?** (yes / no)
10. **Do you have external stakeholders to track?** (board, investors, key customers — yes / no)
11. **What communication style do you prefer from Cowork?** (reply with the number)
    1. Direct and concise (default)
    2. Conversational
    3. Detailed with explanations
12. **Any output preferences I should know about?** (free text, e.g., "no em dashes", "Spanish for family-related notes", "always include a TL;DR" — or reply "none")

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

If a project name slot is empty (user provided fewer than 3), skip that slot. Do not create empty project files.

---

## Step 7: Create the three base schedules

Use `mcp__scheduled-tasks__create_scheduled_task` for each. Read the schedule definition from `schedules/<name>.md` in this repo to get the trigger phrase, cron, and behavior.

| Name | Cron | Trigger phrase |
|------|------|----------------|
| Morning Summary | `0 8 * * 1-5` | "Run my morning summary" |
| Lint Noon | `0 12 * * 1-5` | "Run vault lint" |
| Lint Evening | `0 18 * * 1-5` | "Run vault lint and archive completed tasks" |

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

End with: "Run `cowork check for second-brain updates` whenever you want to pull repo changes."
