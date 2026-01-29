# Queries / Pivots — CASE-001 Brute Force / RDP
Status: Draft (to be updated during implementation)

## Goal
Document the minimal set of queries used to:
1) detect the spike,
2) identify source + targeted account,
3) confirm outcome (lockout/success),
4) check for follow-on activity.

> Add your exact index/sourcetype names later. Keep these queries sanitized.

---

## Splunk (SPL) — Placeholders
### 1) Identify failed logon spike (4625)
```spl
# TBD: search for failed logons (4625) in time window
