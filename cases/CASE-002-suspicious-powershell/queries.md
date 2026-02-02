# Queries / Pivots — CASE-002 Suspicious PowerShell
Status: Draft (to be updated during implementation)

## Goal
Document the minimal set of pivots to:
1) identify PowerShell execution,
2) capture command line + parent/child chain,
3) correlate network/file artifacts (if present).

---

## Splunk (SPL) — Placeholders
TBD: search Sysmon process creation events for powershell.exe
TBD: pivot by parent process and capture command line
TBD: find child processes spawned by PowerShell (if applicable)
TBD: correlate related network connections (Sysmon Event ID 3)

---

## Elastic (KQL) — Placeholders
TBD: find powershell.exe process start events and inspect command line fields
TBD: pivot to parent process + child process fields

---

## Wazuh — Placeholders
TBD: locate relevant events/alerts
TBD: filter by host/user/process name
TBD: capture evidence screenshots
