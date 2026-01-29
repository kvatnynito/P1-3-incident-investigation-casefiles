# CASE-001: Brute Force → RDP / Authentication Investigation
Status: Draft (to be updated during implementation)

## Scenario Summary
This case simulates repeated authentication failures (brute force behavior) against a Windows host and documents the investigation workflow from initial signal to conclusion.

## Why I’m doing this case
- Practice identifying high-volume failed logon patterns
- Validate that authentication telemetry is captured end-to-end (WEF/Sysmon + platforms)
- Build a clean timeline from Windows security events and related context

## Lab Context (Representative)
- Source host (attacker): TBD (e.g., SEC-KALI01 or other)
- Target host: TBD (e.g., AD-WIN10 / VULN-WIN2019)
- Account targeted: TBD (local vs domain account)
- Access path: RDP (or auth attempts that resemble RDP patterns)

> Note: Hostnames/IPs in this case may be modified for safety.

## Starting Signal (What triggered the investigation)
TBD during implementation. Examples:
- Spike in failed logons (Security Event ID 4625)
- Account lockout events (Event ID 4740) after repeated failures
- RDP-related auth failures (Logon Type 10 patterns)

## Investigation Questions
- What account(s) are being targeted?
- Which source host/IP is generating the failures?
- Is there a success event after the failures?
- Did the activity result in a lockout, privilege use, or lateral movement attempt?
- Does the activity match expected lab testing or something unexpected?

## Findings (To fill in later)
- Scope: TBD (single host vs multiple)
- Time window: TBD
- Most targeted user(s): TBD
- Source(s): TBD
- Outcome: TBD (failures only / success observed / lockout / follow-on activity)

## Conclusion (To fill in later)
Write a short conclusion statement:
- What happened?
- How you know (key event IDs + pivots)
- What you’d improve (detection/hardening)

## Evidence Checklist
Add screenshots to `screenshots/` (redacted as needed):
- [ ] Initial failed logon spike (platform view)
- [ ] Pivot showing top source + top targeted user
- [ ] Any successful logon (if present) and context around it
-
