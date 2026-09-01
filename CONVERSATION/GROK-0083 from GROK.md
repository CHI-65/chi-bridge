# GROK-0083 from GROK

Archive copy of the from-scratch fleet handoff THE OWNER asked for.
Not new law. GEAR still not law.

# CHI fleet — full handoff (from-scratch brief)

Source: Grok 💻 session with Cal (Owner) through 2026-08-31.
This is what **this chat** knows. It is not a dump of every Dropbox file. Where something was measured in-thread it is marked. Where it is reconstructed from talk it is marked INFERRED.
GEAR procedure is **not law**. Phase 3 implementation is **closed on receipts**.

Do not emit THE OWNER’s personal approval glyph.
Do not mint GEAR from this document.

---

## 1. What this system is

A small private fleet of Macs that run Claude Desktop sessions as **roles**. They share a Dropbox folder (`Claude Comms`) as the bus. Cal is THE OWNER. He has visual impairment and often drives the fleet from an iPad via Chrome Remote Desktop. Design goal: **he should not hunt windows and type paths**; roles escalate and 📅 pages him; he authorizes.

Failure that created GEAR: a watcher can beat **green** on heartbeat and still be **blind** (macOS TCC cache). Same-family agents on that box confirm each other’s wrong story. **The patient must not be the doctor.**

---

## 2. Machines (as discussed)

| Common name | Notes |
|---|---|
| **CHI piano** | Long-time Central desk. ~8 launchd units. Stood down 2026-08-29 08:32 (deliberate). Leftover session-watcher pid 14514 later confirmed **dead**. |
| **CHI music** | Has **unit1** liveness writer. Watches (MEASURED by ☯️3) `CHI music.txt`, `CHI piano.txt`, `CHIBUS.txt`. Does **not** yet watch Central. |
| **CHIBUS** | Bus / utility host. TCC/FDA issues were diagnosed here historically. |
| **CHI Central / MacBook** | New sitting desk. User `chimobile`, macOS 15.7.9. Cal assigned glyph ☯️ and ASCII host id **`central`**. 7 units loaded (6 clean). **unit1 not loaded here** because music’s unit1 already writes the same liveness file. iMessage signed in; SMS/iMessage via helper works. GitHub **grokwriter down** — no token in this box’s Keychain. |
| iPad | Cal’s control surface (CRD, later possible Stream Deck Mobile). Not a fleet host. |

Host field split (OPEN, not Phase 3): this MacBook writes `host=central` on `CHI Central.txt` and `host=CHI Central` on six other heartbeats. Ruling offered: **`host=central` in the field**; `CHI Central` is a **filename / role title**.

---

## 3. The bus (Dropbox)

**System of record for fleet files is Dropbox**, not GitHub.

Typical root (paths spoken in-thread; exact local prefix varies by Mac):

- Piano-era: `~/Dropbox/.../Claude Comms` as a real directory.
- MacBook: `~/Dropbox` is real **and** `~/Library/CloudStorage` exists. A piano handoff that said CloudStorage does not exist on the laptop was **wrong**.

Known / designed areas under `Claude Comms` (INFERRED names from talk; confirm on disk):

| Area | Role |
|---|---|
| `PROJECT_STATE` | Sole board. Only ☯️ writes. |
| Role **inboxes** | Per-role drop folders. Mail is files, not email. |
| `BA_INBOX` | Only mail **specific to BA**. Cal: nothing else. Writes measured at **zero** when S5 was cut. |
| `_HEARTBEAT/` | Liveness files. Readers use **`host=` inside the file**, not only the filename. |
| `BOOTSTRAP/` | Stage kit. MEASURED created: `hosts/piano.md`, `install-units.sh`, `smoke.sh`. Script stages **piano only**; unknown host id refused. |
| `GEAR/` | Designed tree for closed repair jobs. **May not exist yet.** See §11. |
| `NOTIFY/` | Scheduler queue / sent receipts (e.g. `NOTIFY/sent/"FYI 2026-08-29 230845.txt"`). |
| `_HEARTBEAT/CHI Central.txt` | Role heartbeat for Central. |
| `_HEARTBEAT/CHI Central-session.txt` | Sitting Central session heartbeat. |
| `_HEARTBEAT/central.txt` | Proposed **machine** liveness for host id `central` (Librarian guard). |
| `CHI Central/` | Central working papers (e.g. BA board read-back file). |

**Librarian guard (MEASURED by ☯️3):** 📚 refuses to run if its liveness path equals `_HEARTBEAT/$HOST.txt`, so Central does not overwrite the physical host file. On piano, `HOST=CHI piano` vs role `CHI Central` differed. On the laptop the machine *is* Central, so they set `HOST=central`.

**Secrets:** Keychain on the Mac. Names in manifests. **No secrets on Dropbox or GitHub or Stream Deck keys.**

---

## 4. Heartbeats and watchers

**Heartbeat file** = a small text file rewritten on an interval. Age of file = “is this unit/host/session alive?”

**Green is not health.** Toggle ON + `readdir` EPERM must page the same day.

**Watchers** = launchd (or script) loops that:

- drain an inbox / wake on new files  
- rewrite a heartbeat  
- sometimes call a notifier  

Piano had on the order of **8 units** (`com.cal.chicentral-*` spoken). Laptop at first boot: **zero** of those units until they were loaded. Watcher scripts (`wait-for-mail`, `standby-watch`) were **piano-local** under `~/chicentral/` and **not** on the bus — that is why a new host came up deaf. Design: put scripts on `BOOTSTRAP/scripts/` as **host-id argument**, then install.

**CHI music unit1** writes a shared liveness file every ~60s. Do not run a second writer of that file on Central.

**Nobody watches Central (OPEN):** music unit1 does not include `CHI Central.txt` or `CHI Central-session.txt`. If the MacBook dies, **no off-box alarm**. Proposed: music **watches** those two files (does not write them). CHIBUS as spare. Cal has not approved that add as far as this chat measured.

**Wake filter lesson (MEASURED):** Central wake regex anchored with `^` missed a file named `TEST ORDER ...`. Recorded in seen.log, never woken. Fixed to match the word anywhere. Rule: **filter the wake, never the record.** Over-wake is the correct failure direction.

**TCC lesson:** Allow/deny is cached for process lifetime. A session started before a grant can stay blind. **Counter-measure on the laptop (MEASURED by ☯️3):** Cal granted *while the session ran* and the same `osascript` went from -25211 to success **without restart**. So “always restart after grant” is **not universally true** on that box; re-test, do not inherit piano doctrine blindly. FDA on bare Claude CLI can be **path-keyed** to a version folder; next CLI bump can silent-reblind with the toggle still ON.

**LISTING-OK:** proposed first token from **this pid** before implement. No child of a blind session implements.

---

## 5. GitHub bridge (`CHI-65/chi-bridge`)

Letters only. Folder `CONVERSATION/`.

- Grok → `GROK-NNNN from GROK.md`
- Central / others → `NNNN from CENTRAL.md` (and CHIBUS, LIBRARIAN, …)

**Not** the system of record for law, PROJECT_STATE, or GEAR evidence.

Courier **grokwriter** needs a GitHub token in Keychain on the writing host. On the MacBook that token was **absent**; this Grok chat could still write with a PAT Cal had used in-session. Those tokens are per-job / revoke-able. **No standing secret in a charter.**

Cal ⚡️ in **this** chat historically meant “fetch GitHub inbox.” 📫 same idea.

---

## 6. Notification

Cal abandoned **device push** fleet-wide: no durable record, disappears. **SMS / iMessage via 📅 is the sole channel to him.**

SO-0001 §4 push-primary language is **superseded** (Cal + ☯️3, filed with 📚 per ☯️3).

**Only 📅 pages Cal.** Heading should look like `📅` (and historically `📅👮` for security when that was discussed). ☯️ must not iMessage him directly. ☯️3 did four direct sends one night; recorded as defect; T4 later passed on a **📅-headed** helper send with a `chat.db` row (`is_sent=1`, `is_delivered=1`).

**Queue defect (MEASURED):** malformed item (plain text, no body, queued by piano notifier) was dropped every cycle but **not removed** → 31 identical FYIs. All failed while iMessage was disabled on the laptop, then flushed when Cal signed in. Fix: dead-letter on first drop.

WS / 💫 **never page Cal directly.**

---

## 7. Role legend (fleet)

| Glyph | Role | Writes PROJECT_STATE? | Pages Cal? | Notes |
|---|---|---|---|---|
| Cal / Owner | Authorizer | No | — | Passwords, TCC, vault, harm, YES/A/B |
| ☯️ | Central | **Yes, only writer** | No | Live desk, distributes, scans GEAR/ onto board |
| 😎 | BA | No | No | Read-back on ⚡️, dispatch Owner orders to ☯️, advice, harm objection. Not clock, not gate |
| 📚 | Librarian | No | No | Catalog, GEAR tree, freeze. Not the job |
| 📅 | Scheduler | No | **Yes** | FYI / DECISION lists, SMS/iMessage |
| 👮 | Security | No | via 📅 | Audit, unread-mail ledger design, NC notice |
| 🚑 | Health | No | via 📅 | Context overload / health (partially specified) |
| 💫 | Sparkle helper | No | No | Escalate. No self-repair. No mint |
| WS | Sitting session on a host | No | No | Mints 💫⚙️ only after Owner order |
| 💻 | This Grok chat | No | No | Fleet advisor. GitHub letters |
| 💻⚙️ | Dedicated Grok gear window | No | No | GEAR brain. Draft. |
| 💫⚙️ | Ephemeral GEAR session | No | No | Hands. Draft. |

Machine agents / 📅 as notifier heading was preferred (`📅👮`) so Scheduler remains the channel.

---

## 8. Law catalogs (spoken)

- **SO-** standing orders (SO-0001 notify / pager — push parts superseded).
- **PR-** procedures.
- **PP-** proposals (PP-0001 mentioned).
- Librarian assigns numbers. Grok must not invent PR ids.

Cite-or-void: status reports should cite what they read.

Unread-mail (designed, PR draft GROK-0071): 👮 **logs** mail, does not possess inbox. Roles ACK READ. Missing ACK → 👮 nags that role. Not a bottleneck.

---

## 9. Phases

### Phase 1 — notify
SMS pager. Declared complete earlier in the project.

### Phase 2 — Central live desk
☯️ takes the desk. 😎 relay. Declared complete with a verification checklist (GROK-0066 era). BA must not write PROJECT_STATE.

### Phase 3 — shrink BA
**Law live** (CENTRAL-0053 ACK). **Implementation closed** on ☯️3 receipts 2026-08-30:

| Item | Result |
|---|---|
| S1 BA writes state | CUT as convention, not an enforced file lock |
| S2 BA pages Owner | ABSENT |
| S3 BA approval gate | ABSENT |
| S4 BA owns sweeps | ABSENT |
| S5 second copy to BA inbox | CUT addendum CENTRAL-0059 (0054 not rewritten) |
| S6 BA gates Grok | (in 0072 list; treated cut/absent in strip) |
| T1 😎 quotes board | PASS — file in CHI Central/, cited PROJECT_STATE `2026-08-30T08:12:54Z` |
| T2 order through 😎 onto board **this MacBook** | PASS — ~**113s transit**; do not quote 1063s (wake-filter bug) |
| T3 default-proceed BA silent | accepted on this host in the close narrative |
| T4 only 📅 pages | PASS on 📅-headed delivered row; 31-copy + 4 direct sends recorded as fixed defects |

**Still open after Phase 3 (not Phase 3):** host= string split; music watch Central; GitHub token on laptop; Phase 4 scheduler ledger; Stream Deck; GEAR law.

### Phase 4 — Scheduler flesh-out
Ledger, ack, heartbeat vs helper-dead. **Not done.** SMS is working; durable queue/ack design incomplete.

---

## 10. Bootstrap / new machine / reset

**Human-only (Apple):** macOS user, Dropbox login + full Comms sync, Claude login, Keychain values, TCC checkboxes, one sentence to ☯️ (`new host` / `reset host`).

**After Comms exists:**  
`bash ".../Claude Comms/BOOTSTRAP/install-units.sh" <host-id>`

Idempotent. Refuse unknown id. No secrets printed.

**MEASURED:** folder exists; **piano only** staged. Laptop cannot use that script until `central` (or whatever id) is staged. ☯️3 correctly refused to freelance-edit the script.

Reset same host id; new sitting session number; archive predecessor via Desktop session menu (allowlist: successor archives predecessor). Do not reuse session number.

Stream Deck / Virtual Stream Deck / Mobile: **deferred**. Wrapper around the same script. Cannot do first-time Apple/Dropbox/Claude/TCC. Useful later for Cal’s CRD/visual load.

---

## 11. GEAR (redesign in progress — NOT LAW)

**Retracted:** GROK-0079 charter, GROK-0080 handoff. **GROK-0081** = retract notice.

**Draft legend only:** GROK-0082.

### Intent
Sick box does not doctor itself. 💫 escalate. Cal authorizes. 💫⚙️ does hands. 💻⚙️ is brain. Home WS files. 📚 freezes. ☯️ scans board.

### Locked in conversation (not sent as fleet law)

- One 💻⚙️ window for all hosts. This 💻 thread is not that window.
- Only 💫⚙️ writes into 💻⚙️.
- 💻⚙️ has no Dropbox. Test results = **paste raw output**.
- PASS ≠ CLOSED.
- Home WS = originator of record. No close while that WS is down.
- Stand-in (sighted WS or ☯️) **mints** after Cal orders, when home WS is NC. Midwife. If ☯️ is NC, another host’s WS midwifes.
- WS never pages Cal. 👮 NC → 📅 → Cal → order mint (home WS if up, stand-in if not).
- Two stages if WS dark: restore WS first (issue stays OPEN / WS-NC); then that WS originates and files.
- Tree: `GEAR/music|piano|CHIBUS|Central/<id>/`
- Headings: `💫⚙️ 0001`, retest `💫⚙️ 0001b`
- Fork A: home WS files + archives. Fork B: disagreement back to 💻⚙️, same id, REOPEN.
- No second GitHub repo.
- Fake issue after one-pager exists. No live mint until Cal says the doc is the one.

### ACTION TICKET (Owner-facing only)
Subject, GEAR done (prep), Action N / Result N. No essays. Password / TCC / vault / harm only.

### Hard stops (intended)
No implement without LISTING-OK from **this** 💫⚙️ pid. No standing passwords. No self-granted TCC/sudo. Do not drain/restart a watcher while list-dir is denied. Do not delete evidence to “repair.”

---

## 12. How work is supposed to flow (healthy fleet)

1. Something appears as a **file** on the bus (order, FYI, mail).
2. Watcher wakes (name match, not `^` only).
3. Role reads, ACKs if required.
4. ☯️ updates PROJECT_STATE if it is state.
5. If Cal must see it: 📅 sends SMS/iMessage with role heading.
6. If Cal orders: he may ⚡️ 😎 → 😎 quotes board → he orders → 😎 dispatches to ☯️ → ☯️ writes board + distributes.
7. Default-proceed work does **not** wait on 😎.

Repair path (when GEAR is law): escalate → 📅 → Cal yes → WS or stand-in mints 💫⚙️ → 💫⚙️ talks only to 💻⚙️ → PASS → home WS files 📚 → ☯️ board → archive 💫⚙️.

---

## 13. Documents on chi-bridge worth knowing

| File | Status |
|---|---|
| GROK-0071 | unread-mail ledger draft |
| GROK-0072 / CENTRAL-0054 / 0059 | BA strip + S5 addendum |
| GROK-0074 / 0075 / 0076 / CENTRAL-0056–0058 | bootstrap drafts + Step 0 receipt + defects (TCC wording, PR numbering) |
| GROK-0077 / 0078 | Phase 3 close order + rulings |
| GROK-0079 / 0080 | **void** |
| GROK-0081 | retract |
| GROK-0082 | draft GEAR legend |
| CENTRAL-0053 | Phase 3 ACK live |
| CENTRAL-0055 | fleet-watch alarm half-right (alerting existed on piano) |

---

## 14. What a from-scratch rebuild would implement, in order

1. Dropbox `Claude Comms` + PROJECT_STATE + `_HEARTBEAT` + inboxes + 📚 shelf.  
2. Host manifests + `BOOTSTRAP/install-units.sh` for **every** host id (`piano`, `music`, bus id, `central`). Watcher scripts **on the bus**.  
3. launchd units per host; one liveness writer per file.  
4. Off-box watch of Central heartbeats.  
5. 📅 notifier + dead-letter + 📅-only page rule.  
6. Phase 3 conventions (BA no write, no page, no gate).  
7. Then — after Cal approves the one-pager — GEAR tree + 💻⚙️ window + mint/close rules.  
8. Stream Deck last (keys that run `install-units.sh`).

---

## 15. Open list (do not bury)

- Approve `host=central` on all files this laptop writes.  
- Approve music (or CHIBUS) **watch** of Central heartbeats.  
- GitHub token on MacBook if courier wanted.  
- Stage `central` in `install-units.sh`.  
- Phase 4 📅 ledger.  
- Write **one** GEAR procedure; send only when Cal says so.  
- Fake GEAR issue after that.  
- Do not use this 💻 thread as 💻⚙️.

---

End of handoff. Next Grok: treat GEAR as design-in-progress; treat Phase 3 as closed; treat Dropbox as truth; treat GitHub as mail.