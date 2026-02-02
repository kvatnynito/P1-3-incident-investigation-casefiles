# Elastic (Queries)
Status: Draft (to be updated during implementation)

Elastic is another place where I **store and search logs**.
Instead of “searches,” Elastic usually refers to them as **queries** (commonly written in **KQL**).

I use Elastic to answer the same types of questions as Splunk:
- “What happened?”
- “Which host/user was involved?”
- “What changed after the suspicious activity started?”

---

## What’s inside this folder

### `validation-queries.md`
Quick checks to confirm Elastic is receiving events and that fields look right.

Examples:
- Windows Security events exist
- Sysmon events exist
- Key fields like host/user/source IP are present
- Timestamps line up with the endpoints

### `case-queries.md`
Queries grouped by case (CASE-001, CASE-002, etc.).
These are the step-by-step pivots I used during each investigation.

---

## How this connects to `/cases`
Each case includes a `queries.md` file that documents the investigation pivots.
Those case notes should point back here for the Elastic-specific version.

---

## Current status
These are templates/placeholders until the lab is implemented.
Once Elastic ingestion is working, I’ll replace the placeholders with real KQL queries.
