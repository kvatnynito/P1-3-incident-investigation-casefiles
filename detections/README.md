# Detections

This folder is my **security “toolbox”** for investigating what happened in the lab.

When something looks suspicious (like brute force login attempts or weird PowerShell activity), I use:
- **Searches** (Splunk)
- **Queries** (Elastic)
- **Notes / filters** (Wazuh)

…to answer questions like:
- Who did it?
- Which computer was targeted?
- When did it start?
- Did it succeed?
- What happened next?

---

## How this connects to the case folders
The `/cases` folder contains complete write-ups (CASE-001, CASE-002, etc.).
Each case includes a `queries.md` file that links to the searches/queries I used.

Note: The searches/queries/notes in this folder are currently templates. I’ll fill them in with working content as I implement CASE-001 through CASE-003 in the lab.

- **Cases = the story**
- **Detections = the tools used to find the facts**

---

## Folder layout (what each tool does)
### `splunk/` (Searches)
Splunk is used to search through events (logs) using SPL.
This folder contains:
- validation searches (to confirm logs are arriving)
- case searches (pivots I used during investigations)

### `elastic/` (Queries)
Elastic is another tool that stores/searches logs (commonly using KQL).
This folder contains:
- validation queries
- case queries

### `wazuh/` (Notes)
Wazuh helps monitor systems and generate alerts based on rules.
This folder contains:
- validation notes (how I confirm visibility)
- case notes (which alerts/rules helped during the investigation)

---

## Two types of content you’ll see here
### 1) Validation (Are logs flowing?)
Before investigating anything, I first confirm the lab is actually sending logs.
Example checks:
- Do I see Windows Security events?
- Do I see Sysmon events (process/network)?
- Are timestamps correct?

### 2) Case pivots (How I investigate)
These are step-by-step searches to move through an investigation.
Example pivots:
- show failed logons → find the most targeted user → find the source IP → check if a success happened

---

## Safety / Sanitization
This repo is public, so I avoid posting anything that could expose my home network.

Do NOT include:
- WAN/public IPs, domains/DDNS, VPN details
- passwords, API keys, tokens, secrets
- full exports/backups that contain sensitive info

OK to include (generally):
- representative private IP ranges (10.x / 172.16–31 / 192.168.x)
- sanitized hostnames/usernames
- cropped screenshots showing the workflow

---

## Current status
Right now these are templates/placeholders so Future Me can fill them in while building the lab and completing each case.
