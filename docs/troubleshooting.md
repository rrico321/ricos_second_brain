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

## Templates ask the same question twice or land in the wrong folder

Each template (Daily Note, Meeting Note, Bug Report, 1on1 Prep) self-routes — the Templater script at the top of the file renames the note and moves it to the correct folder automatically. You should be prompted **once** for any user input (e.g., the meeting title, the direct report's name) and the note should land in `Daily Notes/`, `Meeting Notes/`, `Issues/`, or `1on1s/<Name>/` with no further action.

If you're being prompted twice for the same value, or the note is staying wherever you created it:

1. **Confirm Templater is configured to point at `Templates/`.** Settings -> Templater -> "Template folder location" should be `Templates`.
2. **Confirm "Trigger Templater on new file creation" matches your preference.** With self-routing templates, this toggle doesn't matter — the templates relocate themselves regardless. With Folder Templates (manual config alternative), this needs to be ON.
3. **Confirm the target folder exists.** `tp.file.move()` will fail if the destination folder doesn't exist. The 1on1 Prep template, for example, requires `1on1s/<Name>/` to exist — this folder is only created during SETUP if you said yes to managing people. If the folder is missing, ask Cowork to create it: "create a 1on1s folder for <Name>."
4. **Confirm you're using `Create new note from template`, not `Insert template`.** The Insert command pastes into the current note without creating a new file, so `tp.file.move()` has nothing to move.

### Manual configuration alternative (Folder Templates)

If you'd rather use Templater's built-in Folder Templates feature instead of self-routing scripts:

1. Settings -> Templater -> Folder Templates -> Add New
2. Map each folder to its template:
   - `Daily Notes` -> `Templates/Daily Note Template`
   - `Meeting Notes` -> `Templates/Meeting Note Template`
   - `Issues` -> `Templates/Bug Report Template`
   - `1on1s` -> `Templates/1on1 Prep Template`
3. Enable "Trigger Templater on new file creation"
4. Now any file you create *inside* one of these folders auto-applies the matching template.

The shipped templates work either way — Folder Templates and self-routing scripts compose cleanly.

## Tasks query block is empty

The Tasks plugin needs to be enabled. Settings -> Community plugins -> Tasks. The query block reads emoji metadata natively.

## Cowork can't write to my vault

Check OneDrive sync status. If the folder is offline, Cowork can't reach it. Right-click the folder -> Always keep on this device.

## I deleted CLAUDE.md by accident

Restore from OneDrive version history (right-click the file -> Version history -> Restore).

If that fails, re-run SETUP.md - it will detect the missing file and re-create it. Your other content is untouched.
