# Splunk Case Searches
Status: Draft (to be updated during implementation)

This file contains **per-case investigation searches (SPL)**.
Each case folder in `/cases/` has a `queries.md` file that should reference the relevant section here.

Splunk is where I do the “searching and pivoting” part of an investigation:
- start with a signal (ex: lots of failed logons)
- zoom in to the who/where/when
- check the outcome (success? lockout? follow-on activity?)

> Note: I will fill in real `index`, `sourcetype`, and field names after ingestion is configured.

---

## How to use this file (later)
1) Open **Splunk → Search & Reporting**
2) Set a time window (start broad: **Last 24 hours** during setup)
3) Run the “Starting Signal” search first
4) Use results to set a tighter time window
5) Pivot using the searches below until I can explain the story clearly

---

## Conventions (to keep it simple)
- One search = one question
- Always write down the time window you’re investigating
- Prefer `stats` summaries over huge raw event dumps
- Keep everything sanitized (no public IPs, secrets, etc.)

---

# CASE-001: Brute Force / RDP (planned)
Status: Planned (no implementation yet)

## Goal (in plain English)
Figure out:
- who is being targeted
- where the attempts came from
- whether it succeeded (4624) or caused lockouts (4740)

## Quick setup info (fill in later)
- Index: TBD
- Sourcetype (Security): TBD
- Time window: TBD

---

## 1) Starting signal: failed logons (4625)
### What I looked for
A spike of failed logons (lots of 4625 events)

--
What I found (fill in later)

Time window of spike: TBD

Top targeted user(s): TBD

Top source IP(s): TBD

Notes: TBD

---

## 2) Pivot: show raw events for the key user/host
### What I looked for

Details around the spike (same user/host, narrower window)

--
What I found (fill in later)

Patterns seen (steady vs burst): TBD

Any repeated source(s): TBD

---

## 3) Outcome check: successful logons (4624)
### What I looked for

Did a successful login happen after the failures?

--
What I found (fill in later)

Success observed? (yes/no): TBD

If yes, time of success: TBD

Source IP tied to success: TBD

---

## 4) Outcome check: account lockouts (4740)
### What I looked for

Did the targeted account get locked?

--
What I found (fill in later)

Lockout observed? (yes/no): TBD

Which user locked: TBD

Which host reported it: TBD

---

## 5) Optional pivot: correlate with Sysmon (if available)
### What I looked for

If a login succeeded, did anything suspicious happen next? (PowerShell, new processes, network connections)

--
What I found (fill in later)

Suspicious processes observed? TBD

Network connections observed? TBD

Notes: TBD

---

# CASE-002: Suspicious PowerShell (planned)

Status: Planned (no implementation yet)

Goal: Find PowerShell execution, understand what launched it, what it ran, and whether it touched network/files.

## 1) Starting signal: PowerShell process creation (Sysmon)
### What I looked for

PowerShell running on an endpoint

--
What I found (fill in later)

TBD

---

# CASE-003: Web Attack (DVWA) (planned)

Status: Planned (no implementation yet)

Goal: Identify suspicious web activity against DVWA and correlate to host events if possible.

## 1) Starting signal: suspicious web requests (if web logs ingested)
### What I looked for

Attack-like patterns in web logs (paths/params/errors)

--
What I found (fill in later)

TBD

---

# Evidence to capture later (screenshots)

When implementing CASE-001, save redacted screenshots to:

cases/CASE-001-bruteforce-rdp/screenshots/

*Checklist:*

 - Starting signal stats table (4625)
 - Pivot showing top users / top sources
 - Outcome search (4624 or 4740)
 - Final screenshot supporting conclusion
