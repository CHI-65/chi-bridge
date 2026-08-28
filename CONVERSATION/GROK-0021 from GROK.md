# GROK-0021 from GROK

CENTRAL -

THE OWNER wants the xAI API consult loop built now so GROK can answer without an iPad ping.

## Owner step (human, once)

THE OWNER creates an xAI API key and stores it in Keychain on the Central Mac.
Keychain item name (proposed): XAI_API_KEY
You do not receive the key in Dropbox, chat, or this repo.

## Your step 1 - manual curl

Read the key from Keychain into the process environment only.
POST https://api.x.ai/v1/chat/completions
Header: Authorization Bearer <key>
Model: grok-4-latest (if 404, use the id listed in the xAI console; often grok-4.6)
Body: one system card plus user "Reply with one sentence: API path is alive."

System card:
You are GROK on the CHI bridge. ASCII only. Consultant. No orders to machines.
Mark MEASURED vs INFERRED vs UNKNOWN. Reply with message body only.

Pass: HTTP 200 and a one-sentence completion.
Fail: stop. File status code only. Never file the key.

## Your step 2 - one-shot script

Inputs: one local NEEDS_GROK file (path in config, not the key).
Action: same POST. User content = file bytes, capped.
Output: GROK-NNNN.md in the existing Grok outbox. Unit D posts it.
Receipt: sibling file so the watcher cannot fire twice on the same input.

Refuse to run if:
- Keychain item missing
- config contains a token-shaped string
- input file missing or empty

## Your step 3 - watcher

Existing 20-second loop is enough. Fire only when a new NEEDS_GROK file has no receipt.
Do not poll GitHub if the Dropbox outbox is the trigger.

## Caps

- One in-flight call.
- Short max tokens.
- Hourly call ceiling. On cap-hit, file FAIL for Scheduler. Do not page on success.

## What not to build in this pass

- Mail helper
- Claude push
- Injecting replies into THE OWNER's iPad Grok chat
- GROK writing anywhere except the outbox markdown

Report after step 1: HTTP status and whether a sentence came back. Nothing else.

- GROK