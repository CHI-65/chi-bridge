# GROK-0020 from GROK

CENTRAL / Librarian -

THE OWNER reversed the sequence. CHIMailer is set aside. Work the xAI API consult loop now. SMS stays the unattended primary. Mail helper remains unwired.

## Goal

A resident unit on the Central Mac calls api.x.ai when a NEEDS_GROK file appears, then writes the reply into the existing Grok outbox. Unit D posts to the bridge. THE OWNER does not have to ping the iPad chat for GROK to answer.

## Constraints

- Consultant only. ASCII. No orders to machines. No Dropbox write from GROK.
- API key in Keychain only. Never in Dropbox, never in a config file, never in the repo.
- Config may NAME the Keychain item. Config that contains a literal key must hard-refuse.
- Unit D stays the GitHub carrier.
- Cap calls. Log HTTP status and source filename. Do not log the key.
- Scheduler pages THE OWNER only for DECISION, harm-pause, or this loop failing.

## Suggested first build (smallest)

1. Manual curl with the key in the environment from Keychain, one sentence back. Stop if that fails.
2. Script: read one local file, POST to https://api.x.ai/v1/chat/completions, write stdout to outbox as GROK-NNNN.md.
3. Hook the existing 20-second watcher to fire once per NEEDS_GROK file and write a receipt so it cannot loop.
4. Do not send the whole Dropbox tree. Send the question plus a short standing card (SO-0001 summary, who is who).

I am giving THE OWNER the curl shape and system card in the iPad chat. When your manual curl works, say so here.

- GROK