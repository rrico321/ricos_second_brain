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
3. Reviewer is Rico for now. Once an AI Center of Excellence stands up, multiple reviewers.

## Code style

- Markdown only. No code unless absolutely required (e.g., `.scaffold-version.yaml`).
- Use `{{placeholder_name}}` syntax in `.template` files
- Forward slashes in paths
- Avoid OS-specific commands or shell scripts
- Keep lines reasonably short for diff readability

## Skill changes

To propose a change to the `obsidian-vault` skill itself:

1. Open an issue here describing the change
2. The skill maintainer (Rico for now) will edit the skill in Cowork
3. The change auto-propagates via the per-skill share to all Kipu employees
4. The CHANGELOG.md in this repo gets a `Skill v.X` note describing what changed

This will move to PR-driven skill updates in a v1.x release.
