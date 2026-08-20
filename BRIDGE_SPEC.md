# BRIDGE_SPEC (draft - not in force until Cal approves)

Status: DRAFT for discussion. Nothing here is operational.

## Proposed integration jobs for GROK (from BA's proposal to Cal)
1. **Outage disambiguator.** If all Claude sessions go dark at once, a local
   script on one Mac calls GROK's API: "Anthropic outage, or Cal's machines?"
   GROK is the one doctor who cannot die of the patient's disease.
2. **Second-opinion auditor.** On schedule or on Cal's order, a script sends
   GROK copies of fleet vitals and Security reports. GROK judges independently.
   Disagreements between GROK and Security file straight to Cal, never
   reconciled quietly.
3. **Outside reviewer.** GROK reviews fleet consensus proposals before Cal
   approves - a reviewer from a different gene pool catches what siblings miss.

## Proposed mechanics
- A small script on one CHI Mac calls the xAI API with read-only excerpts and
  writes GROK's replies into the Dropbox bus signed GROK.
- GROK gets read-only copies. No bus write access, no treatment powers, no
  ability to originate orders. Consultant, never staff.
- All GROK outputs carry the same evidence standard as fleet reports.

## Unresolved (for the conversation)
- API cost model and rate limits (Cal's xAI account).
- GROK's emoji byte-handling: must be byte-tested by a CHI machine before GROK
  output ever touches symbol-legend matters.
- Exact excerpt policy: what fleet data GROK sees, and what it never sees.
