# Wazuh (Notes)
Status: Draft (to be updated during implementation)

Wazuh is used for **monitoring systems and generating alerts** based on rules.
Instead of thinking of Wazuh like “searching logs,” I treat this folder like my **investigation notes**
for what Wazuh showed me (alerts, rule IDs, and what filters I used).

---

## What’s inside this folder

### `validation-notes.md`
Steps/checklist I use to confirm Wazuh visibility is working.

Examples:
- Are agents connected (if I’m using agents)?
- Do I see Windows events or forwarded logs?
- Do alerts appear when I trigger test activity?
- Are timestamps correct?

### `case-notes.md`
Per-case notes about what Wazuh showed during the investigation.

Examples:
- Which alerts triggered first
- Which rule IDs were involved
- What filtering/pivots helped confirm what happened
- Any tuning notes (sanitized)

---

## How this connects to `/cases`
Each case has a `queries.md` file.  
If Wazuh helped in that case, the case should reference notes here.

---

## Current status
These are templates/placeholders until the lab is implemented.
As I run scenarios, I’ll add screenshots (redacted) and note which alerts/rules were useful.
