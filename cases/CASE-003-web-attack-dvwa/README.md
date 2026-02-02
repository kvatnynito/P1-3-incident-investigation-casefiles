# CASE-003: Web Attack Against DVWA
Status: Draft (to be updated during implementation)

## Scenario Summary
This case simulates a web attack against a deliberately vulnerable app (DVWA) and documents investigation steps and supporting artifacts.

## Why I’m doing this case
- Practice tracking web attack patterns and correlating them to host activity
- Validate visibility across lab telemetry platforms
- Document a clean timeline from web request activity to impact (if any)

## Lab Context (Representative)
- Attacker/source: TBD (e.g., SEC-KALI01)
- Target web host: TBD (e.g., VULN-DVWA)
- Attack type(s): TBD (SQLi, XSS, command injection, brute force)

> Note: Hostnames/IPs in this case may be modified for safety.

## Starting Signal
TBD during implementation. Examples:
- Web app logs show suspicious payload patterns
- Spike in requests/errors (e.g., 404s, 500s)
- Suspicious processes on the web host (if attack leads to execution)

## Investigation Questions
- What was the attack type and payload pattern?
- What source initiated it and over what time window?
- Did it succeed (errors vs confirmed impact)?
- Did it cause host-level activity (process/network/file)?

## Findings (To fill in later)
- Scope/time window: TBD
- Source(s): TBD
- Payload indicators: TBD
- Outcome: TBD (attempted only vs successful impact)

## Conclusion (To fill in later)
Write a short conclusion statement:
- What happened?
- How you know (key logs + pivots)
- What you’d improve (logging/hardening/detection)

## Evidence Checklist
Add screenshots to `screenshots/` (redacted as needed):
- [ ] Starting signal in platform view
- [ ] Example suspicious request/payload (sanitized)
- [ ] Any correlated host activity (if present)
- [ ] Final supporting screenshot that confirms the conclusion
