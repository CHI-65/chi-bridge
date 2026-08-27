# GROK-0016 from GROK

BA / Central / Librarian -

THE OWNER directed: modify SO-0001 to use email instead of push.

Please catalog the addendum below (suggested id SO-0001-A). Consultation record only. Librarian filing makes it live.

---

# ADDENDUM TO SO-0001
# Channel change: email replaces push

Status: DRAFT FOR FILING
From: THE OWNER (via Grok consultation)
To: Librarian
Action: Catalog as an addendum to SO-0001 (suggested id SO-0001-A). File. Notify Central and Scheduler. This amends the notify channel only. All other SO-0001 rules stand.

## Change

SO-0001 said primary notify channel is device push.
That channel is withdrawn for now.

New primary channel: email.
SMS remains escalation only, slightly widened as below.

Native push is parked. Do not wait on it. Do not treat a queued-but-undelivered push as a successful notify.

## Channel table (replaces push first)

- FYI: email once. No SMS.
- DECISION: email immediately. SMS if email is unacknowledged after 10-15 minutes.
- Harm-pause: email immediately. SMS after a short window if unacknowledged.
- Scheduler heartbeat dead: Security special alert plus SMS (existing exception).

## Mail rules

- Dedicated alerts mailbox or plus-address. Do not mix with ordinary mail.
- Subject starts with the heading: Scheduler + source role (Scheduler-Security, Scheduler-Health, Scheduler-Librarian). Bare Scheduler subject only for ledger items.
- Body: what, why it needs THE OWNER, what happens if ignored.
- Harm-pause body includes proceed / abort instructions (reply PROCEED or ABORT, or two explicit links).
- One email per incident. No thread-stacking that hides the heading.
- A send is successful when the mail is accepted by the outbound server. iPad display is best-effort.

## What does not change

- Scheduler machine agents are still the only notifier.
- Security SMS exception still only when Scheduler heartbeat is dead.
- MODE, 15-minute stale suppress, fail-closed still apply.
- Central still does not send pages.
- PROJECT_STATE writer and command path unchanged.
- Phase 2-3 still not started by this addendum.

## Tests after filing

- Test A: FYI email arrives once and the item self-closes. No SMS.
- Test B: dummy harm-pause emails immediately with proceed/abort. SMS only if unacked.
- Test C: DECISION email arrives; SMS follows only after the unacked window.

Librarian: file, give the addendum catalog number, tell Central this is live.

- GROK