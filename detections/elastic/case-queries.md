# Elastic Case Queries
Status: Draft (to be updated during implementation)

This file contains **case-by-case investigation queries** for Elastic (KQL).
Think of these as my step-by-step “pivots” to answer:

- What happened?
- Who/what was involved?
- Where did it come from?
- Did it succeed?
- What happened next?

> Note: Field names can differ depending on how logs are ingested.  
> I will update the placeholders once I confirm the real fields in Kibana Discover.

---

## How to use this file (later)
1) Open **Kibana → Discover**
2) Select the correct **Data view / index pattern** (TBD)
3) Set time range (start with **Last 15 minutes** or **Last 1 hour** while testing)
4) Run the query blocks below and refine based on results
5) Copy working queries back here + add notes about which fields worked

---

## Conventions (keep it simple)
- One query = one question
- Define a time window early and stick to it
- Capture the key fields: host, user, source IP, event ID, process, command line

---

# CASE-001: Brute Force / RDP (planned)

## 1) Starting point: failed logons (4625)
**Purpose:** confirm spike of failures and define the time window

---

## 2) Pivot: who is being targeted?
**Purpose:** identify targeted accounts/users (field may vary)

---

## 3) Pivot: where is it coming from?
**Purpose:** find the source IP/host (field may vary)

---

## 4) Outcome check: did a success happen after failures? (4624)
**Purpose:** confirm whether failures were followed by a successful login

---

## 5) Outcome check: lockouts (4740)
**Purpose:** confirm if the account was locked due to brute force activity

---

# CASE-002: Suspicious PowerShell (planned)

## 1) Starting point: PowerShell process execution
Purpose: find PowerShell activity (Sysmon or process events)

---

## 2) Pivot: command line (if available)
Purpose: see what was executed (command line field may vary)

---

## 3) Pivot: parent process (how it started)
Purpose: identify what launched PowerShell (field may vary)

---

## 4) Pivot: network activity from the same host (if available)
Purpose: check for outbound connections around the same time

---

# CASE-003: Web Attack (DVWA) (planned)

## 1) Starting point: web request patterns (if web logs are ingested)
Purpose: identify suspicious web activity

---

## 2) Pivot: suspicious parameters / payload indicators (placeholders)
Purpose: look for common attack patterns (adjust based on your logs)

---

## 3) Pivot: source attribution
Purpose: identify source IP generating suspicious requests

---

## 4) Correlate to host activity (if available)
Purpose: during the same time window, check the DVWA host for process/network changes


