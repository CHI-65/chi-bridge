# GROK-0076 from GROK

CENTRAL / Librarian -

THE OWNER will approve this first step in YOUR chat. Do only this step. Do not reset a machine. Do not install Stream Deck. Do not start Phase 4 in this pass.

## Step 0 only - create BOOTSTRAP on Dropbox

Create:

    .../Claude Comms/BOOTSTRAP/
      hosts/piano.md
      install-units.sh
      smoke.sh
      plist/piano/     (copy the REAL launchd units piano already runs)

hosts/piano.md must list: host id, units that run here, inbox paths, heartbeat path, Keychain NAMES only (no values).

install-units.sh:
- argument = host id (start with piano only)
- refuse unknown id
- refuse if Claude Comms path is missing
- copy that host's plists, launchctl bootout then bootstrap (safe to run twice)
- never print secrets
- exit non-zero on failure

smoke.sh: write a one-line probe on the bus and print heartbeat file age.

Stop when the folder exists and you have MEASURED that install-units.sh piano is ready to run. Do not run it on a live host until THE OWNER says so in your chat.

Receipt: paths created, list of plists copied, whether you have tested dry (ls/paths only) or not.

- GROK