# Machine bootstrap — two procedures
Owner draft for Librarian to catalog as one PR (or two PR numbers if they prefer).
Grok consultant text. Owner approves in Central chat. Do not reset a host from this file.

## Goal
Owner does only what Apple and vendors force a human to do.
Everything after Dropbox is mounted is a script on the bus.

## Stage on Dropbox first (one-time, Central + Librarian)
Put a folder on the bus, e.g. `/Claude Comms/BOOTSTRAP/`:
- `hosts/<id>.md` — manifest for piano, music, bus
- `install-units.sh` — copies launchd plists from the bus into ~/Library/LaunchAgents and load them
- `first-read.sh` — prints paths of SO-0001, this PR, host manifest, PROJECT_STATE, legend
- `smoke.sh` — writes a heartbeat probe and a one-line bus file
- `plist/` — the actual unit files, one subfolder per host
No secrets in that folder. Keychain names only, in the host manifest.

Terminal guideline: one command after Dropbox is live:
`bash "/path/to/Claude Comms/BOOTSTRAP/install-units.sh" <host-id>`
That script must be idempotent (safe to run twice).

---

## Procedure A — NEW MACHINE
Owner time target: sign-ins only.

1. Power on. Create or sign in macOS user. Wi-Fi.
2. Install Dropbox. Sign in. Wait until `Claude Comms` is fully synced (not “Connecting”).
3. Install Claude Desktop. Sign in to the fleet Anthropic account.
4. Open Keychain. Create items whose NAMES are listed in `hosts/<id>.md`. Paste values once. Close.
5. Open System Settings → Privacy and grant Accessibility + Automation to Claude (and Messages if this host sends SMS). One dialog each. Do not type anything else.
6. Open Terminal. Run ONLY:
   `bash ".../Claude Comms/BOOTSTRAP/install-units.sh" <host-id>`
7. Open Claude Desktop. You do not configure the fleet. Tell Central in chat: `new host <id> first session`.
8. Stop. Central names the sitting session, starts units if the script did not, writes PROJECT_STATE, runs smoke.

If step 6 fails, do not improvise. Send Central the terminal output.

---

## Procedure B — RESET EXISTING MACHINE
Same host id. Prefer this over treating it as new.

1. Reboot first. If Dropbox and Claude still open and Comms is synced, skip to step 5.
2. If the disk was wiped: Procedure A from step 1. Use the SAME host id. Do not invent a new id.
3. If the disk was NOT wiped: confirm Dropbox synced, Claude signed in, Keychain items still present.
4. Re-grant TCC if dialogs appear (common after reset). No other settings.
5. Terminal, same one command:
   `bash ".../Claude Comms/BOOTSTRAP/install-units.sh" <host-id>`
6. Tell Central: `reset host <id>`. Central archives the old sitting session (session-row Archive), opens the next number, writes PROJECT_STATE, smoke.

Do not reuse the old session number.

---

## What the install script must do (so Owner types almost nothing)
- Detect host-id argument; refuse if unknown
- Copy only that host's plists
- launchctl bootout then bootstrap (idempotent)
- Write heartbeat path from the manifest
- Exit non-zero if Dropbox path missing
- Never print secret values

## What stays human forever
- Apple ID / macOS user
- Dropbox login
- Claude login
- Keychain values (first time, or new Mac)
- TCC checkboxes
- The one sentence to Central (`new host` or `reset host`)

## Smoke (Central runs, Owner does not)
- Heartbeat file age < 2 minutes
- One test file appears on the bus
- PROJECT_STATE shows host up + new session name
- Scheduler FYI to Owner: host <id> up (reset|new)