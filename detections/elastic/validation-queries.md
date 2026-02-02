# Elastic Validation Queries

This file is my **“is Elastic working?” checklist**.

Before I investigate any case, I use these queries to confirm:
- logs are arriving in Elastic
- timestamps look correct
- key fields exist (host, user, source IP, event IDs)

> Note: I will fill in the real index pattern / data view name once ingestion is configured.

---

## Quick setup info (fill in later)
- **Data view / index pattern:** TBD (example: `logs-*` or `winlogbeat-*`)
- **Time range used for validation:** Last 15 minutes (or Last 1 hour while testing)
- **Main log sources expected:** Windows Security + Sysmon

---

## How to use this file (later)
1) Open **Kibana → Discover**
2) Select the correct **Data view**
3) Set time range to **Last 15 minutes**
4) Run the queries below
5) If something returns zero results, adjust:
   - time range
   - data view
   - field names (Elastic sometimes uses different names than expected)

---

## 1) “Do I have ANY events at all?”
**Purpose:** confirm ingestion is happening (anything shows up)
Expected: You see events in the last 15 minutes.

---

## 2) Confirm Windows Security events are flowing
**Purpose:** confirm Windows Security log ingestion (logons/failures)
Expected: Events appear, especially if you recently logged in/out or triggered failures.

---

## 3) Confirm Sysmon events are flowing
**Purpose:** confirm Sysmon ingestion (process/network)
Expected: Sysmon events appear on hosts where Sysmon is installed.

Sysmon commonly shows:

Event ID 1 = process creation

Event ID 3 = network connection

---

## 4) Confirm failed logons are visible (4625)
**Purpose:** validate auth telemetry for brute force cases
Expected: Results appear after you intentionally trigger failed logins.

---

## 5) Basic field sanity check
**Purpose:** confirm key fields exist so investigations won’t be painful later
Expected: In Discover, clicking an event shows usable fields like host/user/source IP.

Look for these fields in your events (names may vary):

host.name

user.name

source.ip

event.code

process.name / process.command_line (Sysmon)

---

## 6) Timestamp sanity check
**Purpose:** confirm the timeline makes sense across systems
Expected: events appear close to “now” when you generate activity / no massive time drift (hours/days off)
