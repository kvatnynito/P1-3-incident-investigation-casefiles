# Queries / Pivots — CASE-002 Suspicious PowerShell
Status: Draft (to be updated during implementation)

## Goal
Document the minimal set of pivots to:
1) identify PowerShell execution,
2) capture command line + parent/child chain,
3) correlate network/file artifacts (if present).

---

## Splunk (SPL) — Placeholders
```spl
# TBD: search Sysmon process creation events for powershell.exe
