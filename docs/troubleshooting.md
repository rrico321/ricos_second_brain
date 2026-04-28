# Troubleshooting

## SETUP.md fails partway through

Tell Cowork: "resume my second-brain setup from step N" where N is the last step that completed.

If the failure is in Step 4 (file copy), check that the vault path is writable and that no files are locked by another application.

## OneDrive path on Mac

Typical: `/Users/<name>/Library/CloudStorage/OneDrive-KipuHealth/Obsidian`

If you don't see CloudStorage, OneDrive may not be set up to sync that folder. Check OneDrive settings.

## OneDrive path on Windows

Typical: `C:\Users\<name>\OneDrive - Kipu Health\Obsidian`

In Cowork prompts, use forward slashes: `C:/Users/<name>/OneDrive - Kipu Health/Obsidian`

## obsidian-vault skill doesn't show up

For Kipu employees:
1. Open Cowork Settings -> Skills
2. Look in the "Shared with you" section
3. If not present, ask admin to confirm the skill was shared with "Everyone at Kipu Health"
4. Toggle the skill on

For non-Kipu users:
1. Download `releases/obsidian-vault.skill` from the repo
2. Go to claude.ai → Settings → Profile → Claude's skills
3. Drag the file into the upload area
4. Restart Cowork / refresh the session

## Schedules don't fire

- Confirm your machine is on at the scheduled time
- Confirm Cowork is running (not just installed)
- Check the schedule skill: tell Cowork "list my schedules"
- If a schedule is missing, re-run the relevant section of SETUP.md

## Daily Note shows wrong date

Ensure the Templater plugin is enabled in Obsidian: Settings -> Community plugins -> Templater.

## Tasks query block is empty

The Tasks plugin needs to be enabled. Settings -> Community plugins -> Tasks. The query block reads emoji metadata natively.

## Cowork can't write to my vault

Check OneDrive sync status. If the folder is offline, Cowork can't reach it. Right-click the folder -> Always keep on this device.

## I deleted CLAUDE.md by accident

Restore from OneDrive version history (right-click the file -> Version history -> Restore).

If that fails, re-run SETUP.md - it will detect the missing file and re-create it. Your other content is untouched.
