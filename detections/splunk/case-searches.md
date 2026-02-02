# Splunk Case Searches
Status: Draft (to be updated during implementation)

This file contains per-case investigation pivots (SPL).
Each case folder should reference the relevant section here from its `queries.md`.

## How to use this file (later)
When a case is implemented:
1) Identify the correct `index` and `sourcetype` in Splunk
2) Update the SPL templates below with real values
3) Paste the working searches and note any key fields used

## Conventions
- Keep searches small and focused (one question per search)
- Prefer pivots that support a timeline (user → host → process → network)
- Do not include secrets, public IPs, or external identifiers

---

## CASE-001: Brute Force / RDP (planned)
**Goal:** detect a spike of authentication failures, identify source + targeted account, and determine outcome (failures only vs success vs lockout).

### Starting point — failed logons (4625)
**Purpose:** confirm the spike and define the time window  

### Pivot — top targeted users
**Purpose:** identify which accounts are being targeted

### Pivot — top source IPs / hosts ###
**Purpose:** identify where the failures originate

### Outcome check — successful logons (4624) ###
**Purpose:** determine whether a success occurred after failures

### Outcome check — account lockouts (4740) ###
**Purpose:** confirm whether a lockout occurred due to brute forCASE-002: Suspicious PowerShell (planned)

### CASE-002: Suspicious PowerShell (planned) ###
**Goal:** identify suspicious PowerShell execution and related child processes or network calls.

### CASE-003: Web Attack (DVWA/WebGoat) (planned) ###
**Goal:** identify web attack patterns and correlate to host/network telemetry
