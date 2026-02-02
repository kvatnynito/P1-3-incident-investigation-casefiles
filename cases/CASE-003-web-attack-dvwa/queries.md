# Queries / Pivots — CASE-003 Web Attack (DVWA)
Status: Draft (to be updated during implementation)

## Goal
Document pivots to:
1) identify suspicious web activity,
2) isolate source and time window,
3) correlate to host telemetry if applicable.

---

## Splunk (SPL) — Placeholders
TBD: search web/app logs for suspicious patterns (paths/params/payloads)
TBD: pivot by source IP and time window
TBD: correlate to host Sysmon events on the target during the window

---

## Elastic (KQL) — Placeholders
TBD: query web/app logs data view for suspicious request patterns
TBD: correlate with host process/network events (if available)

---

## Wazuh — Placeholders
TBD: locate relevant alerts/events (web host + endpoint telemetry)
TBD: capture evidence screenshots
