# How It Works

The second brain has four primitives. They map to Cowork features.

## 1. Knowledge layer (Obsidian vault)

Plain markdown files on OneDrive. Cross-platform, vendor-neutral. Cowork reads and writes here.

Folder structure is opinionated but not prescriptive. The interview adapts it to your role.

For a folder-by-folder tour of what lives where and why — root files, daily-flow folders, context/reference, knowledge folders, opt-in folders, and how it all flows in a typical week — see **[`vault-anatomy.md`](./vault-anatomy.md)**.

## 2. Routing layer (CLAUDE.md)

A personalized routing file at the vault root. Cowork loads it on every session start. It tells Cowork:

- Who you are
- How you communicate
- Which org rules apply (via Context/Compliance.md reference)
- Which skill to use for which kind of request

## 3. Skill layer (obsidian-vault)

A Cowork skill that knows the vault's conventions, naming rules, task format, plugin syntax (Dataview, Tasks, Templater, Calendar, Excalidraw), and maintenance workflows.

For Kipu employees: this skill is shared via Cowork's per-skill share. Toggle it on in Settings -> Skills.

For non-Kipu: install the `.skill` from `releases/` in this repo via claude.ai → Settings → Profile → Claude's skills.

## 4. Schedule layer

Three scheduled tasks Cowork runs automatically (when your machine is on):

- 08:00 weekdays - Morning Summary
- 12:00 weekdays - Vault Tidy (read-only health check + Inbox flag)
- 18:00 weekdays - Vault Tidy + archive completed tasks

## How a user interacts

Plain English to Cowork. Examples:

- "I had a meeting with X about Y, add it to my obsidian"
- "What are my tasks today?"
- "Tidy my vault"
- "Sort inbox"
- "Check for second-brain updates"

Cowork uses CLAUDE.md to route the request to the right skill, executes, and writes results back to the vault.

## Why Obsidian

- Cross-platform (Mac, Windows, mobile)
- Plain markdown - no vendor lock
- Live wikilinks and graph view
- Plugin ecosystem (Tasks, Dataview, Templater, Calendar, Excalidraw)
- Works offline

## Why CLAUDE.md as the routing layer

CLAUDE.md is loaded automatically by Cowork on every session start. It is the single source of truth for:

- User identity
- Communication preferences
- Skill routing rules
- Compliance gates (via reference to Context/Compliance.md)

This means every session is consistent without per-session repetition.
