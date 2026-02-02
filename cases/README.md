# Case Files

This folder contains incident-style case files generated from my homelab.  
Each case documents the investigation workflow from starting signal → pivots → timeline → conclusion.

## Case Index
- **CASE-001 — Brute Force / RDP**: `CASE-001-bruteforce-rdp/`
- **CASE-002 — Suspicious PowerShell**: `CASE-002-suspicious-powershell/`
- **CASE-003 — Web Attack (DVWA)**: `CASE-003-web-attack-dvwa/`

## Folder Structure (per case)
Each case should include:
- `README.md` — summary, starting signal, investigation questions, findings/conclusion
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
