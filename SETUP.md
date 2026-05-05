# SETUP.md - Bootstrap a Personalized Second Brain

This file is read by Claude Cowork. If you are a human reading this, you don't need to do anything except tell Cowork: `Go to this repo and run SETUP.md`.

## Cowork: read this section in full before starting

You are bootstrapping a personalized Obsidian vault for the user. Walk through every step in order. Ask questions in plain English. Use your file tools (Read, Write, Edit) to operate on files inside the user's vault folder. Use `mcp__scheduled-tasks__create_scheduled_task` to create schedules.

### Critical rules — read these before you announce anything

- **Do NOT announce or summarize what you're about to do across the whole setup before reading each step's full content.** Read each step in order, in full, before acting. Do NOT pre-commit to a plan ("I'll start with Step 1 and ask for your vault path") based on what setup scripts *usually* do — execute what THIS script literally instructs, step by step.
- **Do NOT ask the user for a vault path.** The Cowork session is already bound to a folder — that folder IS the vault location. Your job in Step 1 is to confirm the cwd, not to gather a path.
- **Do NOT show Mac/Windows path examples.** They are explicitly forbidden.
- **Do NOT check whether the path contains "OneDrive" or warn about storage location.** Storage policy lives in `Context/Compliance.md`, not in this setup script.
- **The exact Step 1 confirmation message** Cowork should send is:
  > "I'll build your second-brain vault in **`<folder name>`** (full path: `<absolute path>`). Everything will be written here. Sound right? (yes / no)"
  Substitute the actual folder name and absolute path. Send nothing else as the first message — no Mac/Windows examples, no policy warnings, no fallback options, no questions about the path.

### Never

- **Run shell commands against the user's vault folder.** No `cp`, `rsync`, `mv`, `rm`, shell loops, or any other shell-driven manipulation of the vault. All file operations on the vault must use your native file tools (Read, Write, Edit). *(You MAY use a sandboxed shell — separate from the user's machine — to read this repo, e.g., `git clone` into a temp dir, or `curl` raw files. The constraint is about not touching the user's vault with shell commands, not about how you fetch repo content into your own working memory.)*
- Touch files outside the user's vault folder (on the user's machine)
- Skip the interview
- Assume answers if the user does not respond
- **Batch interview questions.** Do NOT ask multiple questions in one message, do NOT use AskUserQuestion to bundle several questions, and do NOT pre-fill answers from any user profile or memory. The interview must be strictly sequential: one question, wait for the answer, next question.

### Always

- Confirm before destructive operations
- Use forward slashes in paths the user sees
- Translate paths per-OS when actually writing files
- Ask interview questions one at a time, in plain text, in the order listed in Step 3

The user is non-technical. Prefer plain English over jargon.

---

## Step 1: Use the current Cowork working directory as the vault

The vault will be built in the folder Cowork is already bound to. You're confirming, not gathering. The user already chose this location when they opened the project.

### What to do

1. **Detect the current working directory** (the folder Cowork is bound to). This is available from your environment — it does not require user input.

2. **Send exactly one confirmation message** in this format. Substitute the real folder name (basename of the cwd) and the real absolute path. Do not add anything else — no policy warnings, no Mac/Windows examples, no "if not, please provide" fallbacks, no OneDrive checks:

   > "I'll build your second-brain vault in **`<folder name>`** (full path: `<absolute path>`). Everything will be written here. Sound right? (yes / no)"

3. **Wait for the user's reply** before doing anything else.

### Branching on the reply

- **If the user says yes** (or "yep", "go", "looks right", etc.): set the cwd as `<VAULT_ROOT>` and proceed directly to Step 2.

- **If the user says no**: do NOT ask for a different path. Send this message verbatim and stop the script:

  > "No problem. Close this Cowork session, point Cowork at the folder you actually want the vault in, then re-run SETUP.md from there. The vault always builds in whatever folder Cowork is opened on."

### Anti-patterns (do not do these)

- ❌ Announcing the plan before reading each step ("I'll start with Step 1 and ask for your vault path") — read first, then act.
- ❌ "What is the absolute path to your Obsidian vault folder?"
- ❌ "Mac example: `/Users/<name>/Library/CloudStorage/...`"
- ❌ Any OneDrive substring check or "is this on OneDrive?" warning. Vault location policy lives in `Context/Compliance.md`, not in this setup script. The user's IT environment, not the bootstrap, enforces storage rules.
- ❌ Offering the cwd as a fallback option *while still asking for a path* ("If the vault you want is the currently selected folder, just let me know")
- ❌ Asking the user to type, paste, confirm, or correct the path string itself

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

**Why this step has an explicit file manifest below:** GitHub directory listings (`/tree/main/scaffold`) are JavaScript-rendered, so Cowork's `web_fetch` tool sees an empty shell when it tries to enumerate `scaffold/`. Cowork's `web_fetch` also has a URL-provenance guard that only allows fetching URLs that have appeared in conversation context. Both problems are solved by listing every URL explicitly here — once you read this manifest, those URLs are in your provenance set and you can fetch each one.

**Do not try to crawl the `scaffold/` directory.** Use the manifest below as the authoritative file list. If you cannot fetch a listed URL, surface that to the user and stop — do not invent file contents from memory or from descriptions elsewhere in the repo.

### Manifest

For each row, fetch the **Source URL** and write the result to `<VAULT_ROOT>/<Destination>`. Apply the **Action** rule.

Action legend:
- **Template**: strip the trailing `.template` from the destination, substitute every `{{placeholder}}` with the matching interview answer (using the defaults table further down for blanks), then write.
- **Verbatim**: write the fetched content to the destination unchanged.
- **Folder**: do not fetch. Create the empty folder at the destination. (`.gitkeep` files in `scaffold/` exist only to preserve empty folders in Git; they are not copied to the vault.)

| # | Source URL | Destination (relative to `<VAULT_ROOT>`) | Action |
|---|---|---|---|
| 1 | `https://raw.githubusercontent.com/rrico321/ricos_second_brain/main/scaffold/CLAUDE.md.template` | `CLAUDE.md` | Template |
| 2 | `https://raw.githubusercontent.com/rrico321/ricos_second_brain/main/scaffold/Home.md.template` | `Home.md` | Template |
| 3 | `https://raw.githubusercontent.com/rrico321/ricos_second_brain/main/scaffold/index.md.template` | `index.md` | Template |
| 4 | `https://raw.githubusercontent.com/rrico321/ricos_second_brain/main/scaffold/README.md` | `README.md` | Verbatim |
| 5 | `https://raw.githubusercontent.com/rrico321/ricos_second_brain/main/scaffold/Context/.scaffold-version.yaml.template` | `Context/.scaffold-version.yaml` | Template |
| 6 | `https://raw.githubusercontent.com/rrico321/ricos_second_brain/main/scaffold/Context/Compliance.md` | `Context/Compliance.md` | Verbatim |
| 7 | `https://raw.githubusercontent.com/rrico321/ricos_second_brain/main/scaffold/Context/Glossary.md` | `Context/Glossary.md` | Verbatim |
| 8 | `https://raw.githubusercontent.com/rrico321/ricos_second_brain/main/scaffold/Context/Memory.md` | `Context/Memory.md` | Verbatim |
| 9 | `https://raw.githubusercontent.com/rrico321/ricos_second_brain/main/scaffold/Context/context.md.template` | `Context/context.md` | Template |
| 10 | `https://raw.githubusercontent.com/rrico321/ricos_second_brain/main/scaffold/Context/projects.md.template` | `Context/projects.md` | Template |
| 11 | `https://raw.githubusercontent.com/rrico321/ricos_second_brain/main/scaffold/Tasks/Tasks.md.template` | `Tasks/Tasks.md` | Template |
| 12 | `https://raw.githubusercontent.com/rrico321/ricos_second_brain/main/scaffold/Tasks/Archive/Archive.md.template` | `Tasks/Archive/Archive.md` | Template |
| 13 | `https://raw.githubusercontent.com/rrico321/ricos_second_brain/main/scaffold/Templates/Daily%20Note%20Template.md` | `Templates/Daily Note Template.md` | Verbatim |
| 14 | `https://raw.githubusercontent.com/rrico321/ricos_second_brain/main/scaffold/Templates/Meeting%20Note%20Template.md` | `Templates/Meeting Note Template.md` | Verbatim |
| 15 | `https://raw.githubusercontent.com/rrico321/ricos_second_brain/main/scaffold/Templates/Bug%20Report%20Template.md` | `Templates/Bug Report Template.md` | Verbatim |
| 16 | `https://raw.githubusercontent.com/rrico321/ricos_second_brain/main/scaffold/Templates/Task%20Template.md` | `Templates/Task Template.md` | Verbatim |
| 17 | `https://raw.githubusercontent.com/rrico321/ricos_second_brain/main/scaffold/Templates/1on1%20Prep%20Template.md` | `Templates/1on1 Prep Template.md` | Verbatim |
| 18 | — | `Daily Notes/` | Folder |
| 19 | — | `Meeting Notes/` | Folder |
| 20 | — | `Projects/` | Folder |
| 21 | — | `People/` | Folder |
| 22 | — | `SOPs/` | Folder |
| 23 | — | `Issues/` | Folder |
| 24 | — | `Inbox/` | Folder |

Spaces in URLs are URL-encoded (`%20`); spaces in destination paths are literal.

After Step 5 (interview-driven additions), additional folders may be created (`1on1s/<Name>/`, `Strategic Initiatives/`, `Stakeholders/`, `Candidates/`). Those are not in the base manifest above — they're handled by Step 5.

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
| Vault Tidy (Evening) | `0 18 * * 1-5` | "Tidy my vault" |

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
