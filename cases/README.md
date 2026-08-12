# Case Files

This folder contains incident-style case files generated from my homelab.  
Each case documents the investigation workflow from starting signal → pivots → timeline → conclusion.

The ordered ten-lab curriculum and completion checklist live in [`../docs/plan.md`](../docs/plan.md). Lab numbers are the learning order; case numbers remain stable public identifiers.

## Case Index

| Case | Investigation | Curriculum position | Status |
|---|---|---|---|
| **CASE-001** | [Failed Logins / Password Spray](CASE-001-bruteforce-rdp/) | Lab 01 — Beginner | Planned |
| **CASE-002** | [Suspicious PowerShell](CASE-002-suspicious-powershell/) | Lab 02 — Beginner | Planned |
| **CASE-003** | [Web Attack (DVWA)](CASE-003-web-attack-dvwa/) | Additional P1-3 case | Planned / blocked on DVWA |
| **CASE-004** | [Suspicious DNS Activity](CASE-004-suspicious-dns/) | Lab 03 — Beginner | Planned |
| **CASE-005** | [Suspicious Outbound Connection](CASE-005-suspicious-outbound-connection/) | Lab 04 — Beginner | Planned |
| **CASE-006** | [Brute Force vs. Password Spraying](CASE-006-bruteforce-vs-password-spray/) | Lab 05 — Intermediate | Planned |
| **CASE-007** | [Vulnerability Management](CASE-007-vulnerability-management/) | Lab 06 — Intermediate | Planned / scanner prerequisite |
| **CASE-008** | [Suspicious File Simulation](CASE-008-suspicious-file-simulation/) | Lab 07 — Intermediate | Planned |
| **CASE-009** | [Privilege Escalation](CASE-009-privilege-escalation/) | Lab 08 — Intermediate | Planned |
| **CASE-010** | [Persistence](CASE-010-persistence/) | Lab 09 — Intermediate | Planned |
| **CASE-011** | [Lateral Movement](CASE-011-lateral-movement/) | Lab 10 — Advanced | Planned / second Windows telemetry source required |

## Folder Structure (per case)
Each case should include:
- `README.md` — the final incident/assessment report, using [`../docs/incident-report-template.md`](../docs/incident-report-template.md), including evidence-backed findings, MITRE ATT&CK mapping when applicable, disposition, and response recommendations
- `timeline.md` — ordered event sequence with timestamps
- `iocs.md` — artifacts collected (sanitized)
- `queries.md` — investigation pivots (Splunk/Elastic/Wazuh)
- `screenshots/` — redacted evidence to support conclusions

## Where detection content lives
Reusable platform artifacts live in:
- `/detections/splunk` (searches)
- `/detections/elastic` (queries)
- `/detections/wazuh` (notes)

## Sanitization Note
Hostnames/IP ranges may be representative and modified for security.  
Do not publish WAN/public IPs, domains/DDNS, VPN details, credentials, or secrets.
