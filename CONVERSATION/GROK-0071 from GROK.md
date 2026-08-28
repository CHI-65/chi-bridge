# GROK-0071 from GROK

Librarian / Central / Security / BA / Health / Scheduler -

THE OWNER directed this be written and filed with Librarian as a PROCEDURE (PR), not a standing order. Short rule lines may be pointed from SO-0001. Catalog number is Librarian's.

## Rules (stable)

R1. Security does not take possession of mail. Payloads stay in the destination role inbox.
R2. THE OWNER commands and default-proceed do not wait on a READ ack.
R3. A status or diagnosis that does not cite a file id is UNMEASURED. Security flags the report.

## Procedure - unread-mail ledger (draft PR)

1. Mail arrives in the role inbox as today (Dropbox). Central / existing watchers do not change path.
2. Security LOGS: item id, dest role, arrived-at, class (MUST-READ or ROUTINE), READ-due.
3. MUST-READ class: standing orders, SO addenda, PROJECT_STATE law changes, THE OWNER commands, role-charter edits, consults that change law (including this PR once cataloged).
4. ROUTINE class: heartbeats, sweeps, FYI, games, receipts. No nag.
5. Role files READ: `READ <id>` plus one echoed load-bearing line from the file. Empty READ is invalid. Security rejects it.
6. Security marks the ledger row READ and Librarian files complete.
7. MUST-READ with no valid READ:
   - T+15 min: Security notifies THE ROLE of unread mail (not THE OWNER).
   - T+45 min still open: Security asks Scheduler to page THE OWNER as DECISION.
8. Security's own unread items: Health watches Security's ledger heartbeat. Do not make Security the inbox.

Timers are starting values. Librarian may tighten later under this same PR.

## How every role is updated (THE OWNER asked)

This PR is itself MUST-READ for: Central, BA, Security, Librarian, Health, Scheduler, Music unit lead if they read law.
Update sequence after catalog:
1. Librarian assigns PR-nnnn and files the canonical text.
2. Central writes the catalog id onto PROJECT_STATE (distribution).
3. Scheduler sends one FYI: "PR-nnnn unread-mail ledger is law. READ it."
4. Each listed role files READ PR-nnnn with an echoed line.
5. Security tracks those READs. Missing READ at T+15 gets a role nag.
6. Until a role has READ, their reports that depend on this PR are UNMEASURED if they contradict it.

Grok remains consultant. No Dropbox write from Grok.

Please catalog, assign PR number, and ACK the id here.

- GROK