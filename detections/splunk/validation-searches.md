# Splunk Validation Searches
Status: Draft (to be updated during implementation)

This file is my **“is Splunk working?” checklist**.

Before I investigate any case, I use these searches to confirm:
- data is arriving (Windows Security + Sysmon)
- key fields exist (host, user, source IP, event codes)
- timestamps make sense

> Note: I will fill in the real `index` and `sourcetype` values once ingestion is configured.

---

## Quick setup info (fill in later)
- Splunk URL / instance: TBD
- Index used for Windows logs: TBD
- Sourcetype for Windows Security logs: TBD
- Sourcetype for Sysmon logs: TBD
- Time range used for validation: Last 15 minutes (or Last 1 hour while testing)

---

## How to use this file (later)
1) Go to **Search & Reporting**
2) Set time picker to **Last 15 minutes**
3) Run Search #1 first (broad “do I have anything?”)
4) Identify the real `index` + `sourcetype` from results
5) Update the searches below with real values
6) Save 1–2 redacted screenshots as proof of ingestion

---

## 1) Basic check: do I have ANY events at all?
### What I looked for
Any events in the last 15 minutes (to confirm ingestion exists)

--
What I found (fill in later)

Returned events? (yes/no): TBD

Example sourcetype(s) seen: TBD

Example host(s) seen: TBD

---

## 2) Confirm Windows Security events are flowing
### What I looked for

Windows Security log events (logons/failures)

--
What I found (fill in later)

Events present? (yes/no): TBD

Common event codes seen: TBD

Key fields confirmed: host / user / EventCode / src_ip (TBD)

---

## 3) Confirm Sysmon events are flowing
### What I looked for

Sysmon events that show process/network activity

Common Sysmon event IDs:

1 = Process creation

3 = Network connection

--
What I found (fill in later)

Sysmon present? (yes/no): TBD

Which Sysmon EventCode(s) seen: TBD

Key fields confirmed: process, command line, destination (TBD)

---

## 4) Confirm failed logons are visible (4625)
### What I looked for

Windows Security failed logons (useful for brute force investigations)

--
What I found (fill in later)

Any 4625 events? (yes/no): TBD

Top targeted user(s): TBD

Top source IP(s): TBD

Notes: TBD

---

## 5) Quick field sanity check
### What I looked for

That Splunk extracted the fields I need for investigations.

--
What I found (fill in later)

Which fields exist as-is: TBD

Which fields need adjustment/normalization: TBD

---

## 6) Timestamp sanity check
### What I looked for

Events should appear close to when I generate activity.

--
What I found (fill in later)

first_seen / last_seen looked correct? (yes/no): TBD

Any time drift noticed: TBD

---

## Evidence to capture later (screenshots)

**Save redacted screenshots to:**

/screenshots/ (global) if it’s platform-wide

cases/CASE-XXX.../screenshots/ if it’s case-specific

## Checklist:

 - Splunk showing recent Security events
 -  Splunk showing Sysmon events
 -   One validation search result table (fields visible)
