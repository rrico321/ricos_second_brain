# Contributing

This is a private POC repo until stress-tested. Once public, contribution rules apply.

## What we accept

- Improvements to the scaffold templates
- New schedules with clear use cases
- Documentation fixes
- New `docs/` content (especially troubleshooting)
- Suggestions for v1.x role packs (people-manager, executive-leader, finance, sysadmin)

## What we don't accept yet

- Skill source PRs. The `obsidian-vault` skill lives in Cowork's skill manager, not in this repo. v1.x will introduce a `skills/` folder with PR-driven updates.
- New connectors. Connector approval flows through Kipu IT.
- Telemetry, analytics, usage tracking. Not in scope for v0 or v1.

## How to propose a change

1. Open an issue describing the change and the use case
2. If accepted, fork and PR
3. Reviewer is the project owner for now. Once an AI Center of Excellence stands up, multiple reviewers.

## Code style

- Markdown only. No code unless absolutely required (e.g., `.scaffold-version.yaml`).
- Use `{{placeholder_name}}` syntax in `.template` files
- Forward slashes in paths
- Avoid OS-specific commands or shell scripts
- Keep lines reasonably short for diff readability

## Pre-push consistency checklist

Run through this list before pushing. The repo doesn't ship an automated CI script (per the "no scripts" constraint), so consistency is enforced manually until/unless a tiny GitHub Actions yaml workflow is added.

**Version consistency:**
- [ ] `README.md` Status line version matches latest `CHANGELOG.md` entry
- [ ] `scaffold/Context/.scaffold-version.yaml.template` `scaffold_version:` matches latest `CHANGELOG.md` entry
- [ ] `CHANGELOG.md` has an entry for the version you're shipping

**Placeholder integrity:**
- [ ] Every `{{placeholder_name}}` used in a `.template` file is either filled by an interview answer in `SETUP.md` Step 3, or has a default in the Step 4 defaults table
- [ ] No bare `{{...}}` left in non-template `.md` files (would render as literal text in the user's vault)

**Cross-doc consistency:**
- [ ] If you renamed a folder, schedule, or template, grep the whole repo for the old name and update all references (`grep -r "old-name" .`)
- [ ] If you changed an interview Q-number, all `Q\d` references in `SETUP.md` Step 5/6 and `scaffold/Tasks/Tasks.md.template` still point to the right question
- [ ] Schedule names, crons, and trigger phrases in `SETUP.md` Step 7 table match the corresponding `schedules/<name>.md` file
- [ ] Files referenced from `README.md` Documentation section all exist (`docs/*.md`, `CONTRIBUTING.md`, etc.)
- [ ] **`SETUP.md` Step 4 manifest matches the actual `scaffold/` tree.** Cowork can't enumerate `scaffold/` (the GitHub directory page is JS-rendered), so the manifest is the authoritative file list. If you add/rename/remove a scaffold file, update the manifest. Quick verify: `curl -s "https://api.github.com/repos/rrico321/ricos_second_brain/git/trees/main?recursive=1" | python3 -c "import json,sys;[print(x['path']) for x in json.load(sys.stdin)['tree'] if x['path'].startswith('scaffold/') and x['type']=='blob']"` should match the Source URL paths in the manifest.

**Trust hygiene:**
- [ ] If you added a feature that's not yet implemented, it's marked clearly (callout, "planned for v1.x", or in the README "Current Status" table)
- [ ] If you removed a feature, all references to it are gone (FAQ examples, vault-anatomy flow, schedule list, etc.)
- [ ] No personal data (names, vault paths, ticket numbers) snuck into docs that ship to all users

## Skill changes

To propose a change to the `obsidian-vault` skill itself:

1. Open an issue here describing the change
2. The skill maintainer (the project owner for now) will edit the skill in Cowork
3. The change auto-propagates via the per-skill share to all Kipu employees
4. The CHANGELOG.md in this repo gets a `Skill v.X` note describing what changed

This will move to PR-driven skill updates in a v1.x release.
