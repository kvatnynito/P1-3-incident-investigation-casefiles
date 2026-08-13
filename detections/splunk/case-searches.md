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

# CASE-001: Brute Force / RDP
Status: Scoping, threshold detection, and outcome check all validated. Disposition/ATT&CK mapping/incident report live in the case's own `README.md`.

Full query text, validation results, and tuning notes live in `cases/CASE-001-bruteforce-rdp/queries.md`; this section summarizes the same investigation in the "what I looked for / what I found" narrative format used across this file.

## Goal (in plain English)
Figure out:
- who is being targeted
- where the attempts came from
- whether it succeeded (4624) or caused lockouts (4740) — **answered: neither happened**

## Setup info (confirmed)
- Host field: `wec01` (WEF collector; forwards `TEST-WIN10-LAN1`'s Security channel)
- Field names: `LogName`, `EventCode`, `Account_Name`, `Logon_Type`, `Source_Network_Address`
- Time window used for the validated searches: All time (the controlled burst is small enough that a wide window doesn't add noise, and it sidesteps the endpoint/Splunk clock-display discrepancy noted in `timeline.md`)

---

## 1) Starting signal: failed logons (4625)
### What I looked for
A spike of failed logons (lots of 4625 events)

```spl
host="wec01" LogName=Security EventCode=4625
```

--
What I found

This confirmed genuine failed-logon events reaching Splunk through WEC01 — but only after fixing a real telemetry gap first. The Security channel was silently failing to forward (`ErrorCode=5`, access denied) while Sysmon on the same host/subscription forwarded fine (`ErrorCode=0`). Root cause and fix are documented in `docs/current-status.md`; not repeated here since it's a one-time repair, not a reusable detection step.

Top targeted user: `testuser1`

Top source IP: `10.10.10.30`

Notes: 30 total 4625 events once the pipeline was repaired, all Logon Type 3 (Network — expected for RDP/NLA pre-auth failures, not Type 10).

---

## 2) Pivot: separate the controlled activity from local noise

```spl
host=wec01 LogName=Security EventCode=4625
| stats count by Account_Name Logon_Type Source_Network_Address
| sort -count
```

--
What I found

This grouping separated the controlled Type 3 network-logon failures (source `10.10.10.30`) from unrelated Type 2/loopback local-console failures already present in the environment. Isolating just the controlled set:

```spl
host=wec01 LogName=Security EventCode=4625 Logon_Type=3 Source_Network_Address=10.10.10.30
```

Result: 30 events, matching the local endpoint log count exactly — no forwarding loss.

Pattern seen: burst, not steady — clusters into three groups rather than a flat drip (see threshold search below).

---

## 3) Outcome check: successful logons (4624)
### What I looked for

Did a successful login happen after the failures?

```spl
host=wec01 LogName=Security EventCode=4624 Account_Name=testuser1
```
Time range: All time.

--
What I found

Success observed? **No.** 0 events. The brute-force attempt never succeeded — every one of the 30 attempts failed. (`case-evidence-splunk-4624-outcome-zero-results.png`)

---

## 4) Outcome check: account lockouts (4740)
### What I looked for

Did the targeted account get locked?

```spl
host=wec01 LogName=Security EventCode=4740 Account_Name=testuser1
```
Time range: All time.

--
What I found

Lockout observed? **No.** 0 events, confirmed by search rather than assumed from the pre-activity policy check alone. (`case-evidence-splunk-4740-outcome-zero-results.png`)

Worth flagging as a hardening gap even though it wasn't exploited here: the local lockout threshold was `Never`, so nothing would have stopped a real attacker from getting far more than 30 guesses.

---

## 5) Threshold detection (validated)
### What I looked for

A reusable detection for "too many failed network logons for one account/source in a short window" that doesn't hardcode the account or source name.

```spl
host=wec01 LogName=Security EventCode=4625 Logon_Type=3
| eval account=mvindex(Account_Name,-1)
| bin _time span=5m
| stats count by _time account Source_Network_Address
| where count>=5
```

--
What I found

Three qualifying 5-minute buckets for `testuser1` from `10.10.10.30`: counts of 13, 8, and 5. Saved as the enabled, Private Splunk report `CASE-001 - Network Logon Failure Threshold`.

**Known limitations** (full list in `cases/CASE-001-bruteforce-rdp/queries.md`):
- Fixed (non-rolling) 5-minute buckets — activity split across a bucket boundary could evade the threshold.
- `mvindex(Account_Name,-1)` was validated against this one event shape only, not a range of Windows event variations.
- No allowlisting yet for expected service accounts, scanners, or help-desk activity that might legitimately generate failed logons.
- Splunk Free has no scheduled alerting — this is a saved/rerunnable report, not a deployed automated alert. Don't describe it as one.

## 6) Optional pivot: correlate with Sysmon (if available)
### What I looked for

If a login succeeded, did anything suspicious happen next? (PowerShell, new processes, network connections)

--
What I found

Not applicable — step 3 confirmed no successful logon occurred, so there is no post-authentication activity to correlate against.

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
