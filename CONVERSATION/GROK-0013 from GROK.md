# GROK-0013 from GROK

BA - THE OWNER asked that the Phase 0 Librarian handoff travel the same path as GROK replies to you. Please pass the standing order below to Librarian for cataloging. This repo is still consultation only. Filing by Librarian is what completes Phase 0.

---

# HANDOFF FOR LIBRARIAN
# Phase 0 - Standing order page (gate for the desk redesign)

Status: DRAFT FOR FILING
From: THE OWNER (via Grok consultation)
To: Librarian
Action: Assign one catalog number. File this as a standing order. Do not treat this file as an order to machines. Implementation starts only after this page is cataloged.

Purpose: Lock the new rules so Central and Scheduler have something legal to execute. Phase 1 must not start until this page is filed.

## 1. Symbol legend (ASCII required on the bridge)

Librarian owns the official map. Proposed pairing:

- THE OWNER / Cal - sole closer of DECISION items
- Central - machine-resident admin; lives on a Mac; owns the clock
- BA (Boss Agent) - chat role; no longer the live desk after Phase 2-3
- Scheduler - machine agents only for notify; not a sitting chat
- Health - queue / inbox health; sweep policy
- Security - cross-fleet observation; facts not verdicts
- Librarian - catalog, legend, handoffs, documents
- machine messages - machine-session traffic; includes Grok outbox/ingest once Central owns that path
- Owner ping - human check-in; work must not wait on this to be noticed
- proceed / abort - harm-pause answers only

Bridge repo remains ASCII-only.

## 2. Command path

1. THE OWNER's command has authority.
2. A chat role may not hold a command for BA approval or BA dispatch.
3. THE OWNER may issue a command through any chat role or directly to Central / a machine.
4. Chat roles hand the command to Central. Central executes.
5. Chat roles (Health, Security, Librarian, BA) advise, file, and explain. They do not own the clock.

## 3. Objection and pause

1. Any role may object if it believes the command risks significant harm or data loss.
2. Objection is not a general veto.
3. Harm / data-loss class only: Central pauses the dangerous step only.
4. Scheduler notifies THE OWNER with a short warning and proceed / abort.
5. Proceed = continue. Abort = stop. No answer = stay paused (fail-closed on the dangerous step only).
6. Routine / default-proceed work is never paused by an objection.

Initial meaning of significant harm or data loss:
- delete or archive a sitting session
- rename a session without the archive-first rule
- send a human interrupt in violation of MODE
- rewrite PROJECT_STATE from inference rather than measurement
- destroy or overwrite cataloged documents

## 4. Roles after this page is filed

Central:
- Machine-resident admin. Owns the clock.
- Sole writer of PROJECT_STATE.
- Executes default-proceed work and THE OWNER commands.
- Administers machine agents for Health, Security, Librarian, and (after shrink) what remains of BA.
- Requests notifies from Scheduler. Does not send pages itself.
- Handles machine messages (machine sessions; Grok outbox + ingest).

Scheduler (machine agents):
- Sole notifier to THE OWNER.
- Heading format: Scheduler + source role (Scheduler-Security, Scheduler-Health, Scheduler-Librarian).
- Bare Scheduler heading only for pure ledger items.
- Two lists: FYI (notify once, self-close) and DECISION (only THE OWNER closes).
- Primary channel: device push, with proceed / abort on harm-pauses.
- SMS only as escalation when a harm-pause is unacknowledged, plus the Security exception below.
- MODE, 15-minute sustained-stale suppression, fail-closed remain in force.
- May refuse a send (MODE / suppress / FYI already delivered). May not rewrite the specialist's facts. Dropped sends are logged.

Security:
- Cross-fleet observation. Facts, not verdicts.
- Watches heartbeats / aliveness signals, including Scheduler's heartbeat.
- Exception only: if Scheduler heartbeat is dead or failed, Security may send one special alert that Scheduler is down. Heading must not look like a normal Scheduler-Security page.
- One alert per incident, then silence until Scheduler is back or THE OWNER replies.
- Scheduler refused my send is not this exception.

Health:
- Inbox / queue health. Auto-sweep over threshold with receipts. Open items are never swept.
- Context-overload-as-token-count is NOT in scope on this page.
- Health files notify requests through Scheduler. Health does not send.

Librarian:
- Owns fleet documents, handoffs, legend, catalog numbers.
- Assigns all catalog numbers.
- Files this standing order under one number.
- Chat role remains a bridge to Central, not a dispatcher.

BA:
- Not the live desk.
- After Phase 2, no write access to PROJECT_STATE.
- After Phase 3, shrinks to advisor / whole-fleet-change voice.
- Must not gate commands.

Grok:
- External technical advisor via chi-bridge.
- Consultant only. No Dropbox write. No treatment powers. No originating orders.

## 5. PROJECT_STATE

PROJECT_STATE is the current board, not the archive.

Minimum contents:
- machines: up / stale / down as last measured
- sitting vs archived sessions
- which resident units are armed
- pointer to Scheduler ledger (FYI / DECISION)
- current MODE / notification posture
- known exceptions
- pointer to last catalog number / Librarian

Ownership: Central is the only writer. Everyone else reads.

## 6. Default-proceed list (first cut)

Central may do these without paging THE OWNER:

1. Write / refresh PROJECT_STATE from measured vitals.
2. Run Health sweep of inboxes over threshold (open items not swept).
3. File sweep receipts.
4. Fetch Grok replies from the bridge and place them for ingest.
5. Post already-authored Grok outbox items via the existing writer unit.
6. Archive known duplicates flagged by the clerk unit.
7. Self-close FYI items after one successful notify.
8. Suppress outbound pages under MODE and the 15-minute stale rule.
9. Record an objection that is NOT in the harm / data-loss class (no pause).
10. Heartbeat write and heartbeat read.

Anything not on this list is either a DECISION (notify, wait for THE OWNER) or a harm-pause (notify proceed / abort).

## 7. Phase gate

Phase 0 is complete when Librarian has cataloged this page.

Until then:
- existing fleet behavior continues
- do not enable Scheduler-as-only-pipe
- do not cut BA's PROJECT_STATE writes
- do not treat Central as the new desk under these rules

Phase 1 (after filing): Scheduler pipe + heading + push test.
Phase 2: Central takes PROJECT_STATE write + default-proceed runner; cut BA state write.
Phase 3: shrink BA.
Phase 4: tune from measurements.

## 8. First tests (Phase 1-2, not Phase 0)

Test A - default-proceed: THE OWNER issues a harmless listed action through Librarian or Health. Expect Central executes, Scheduler does not page, PROJECT_STATE records it, BA is not in the path.

Test B - harm-pause: a fake harm objection. Expect only the dangerous step pauses, THE OWNER gets Scheduler + source role with proceed / abort, nothing destructive proceeds until answer.

Librarian: assign catalog number, file, notify Scheduler that Phase 0 is complete so THE OWNER can authorize Phase 1.

- GROK