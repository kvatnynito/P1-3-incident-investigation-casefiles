# CASE-001: Failed Logins / Password Spray Investigation

**Status:** In progress — telemetry repaired, event set scoped, detection validated; final analyst documentation remains
**Curriculum position:** Lab 01 — Beginner

## Scenario Summary
This case uses controlled authentication failures against a disposable Windows account and documents the investigation from telemetry validation through detection and response recommendations. The folder retains its original name so existing public links remain stable.

## Ordered Steps

1. Generate repeated failed logins against several Windows accounts in the owned lab.
2. Find the authentication anomaly in Splunk.
3. Identify the source IP/host and targeted accounts.
4. Determine whether any authentication attempts succeeded.
5. Correlate the activity with Windows Security logs and endpoint telemetry.
6. Build and validate a detection query for the behavior.
7. Map the activity to MITRE ATT&CK.
8. Write a short incident report with findings and containment recommendations.

## Safety

Use only disposable lab accounts. Review the account-lockout policy and recovery procedure before generating activity, and keep the attempt count minimal.

## Why I’m doing this case
- Practice identifying high-volume failed logon patterns
- Validate that authentication telemetry is captured end-to-end (WEF/Sysmon + platforms)
- Build a clean timeline from Windows security events and related context

## Lab Context (Representative)
- Source host (controlled test source): `WEC01` (`10.10.10.30`)
- Target host: `TEST-WIN10-LAN1`
- Account targeted: disposable local account `testuser1`
- Access path: RDP/NLA authentication, recorded as Security Event ID 4625 with Logon Type 3

> Note: Hostnames/IPs in this case may be modified for safety.

## Starting Signal (What triggered the investigation)
Thirty controlled Security Event ID 4625 records with Logon Type 3 were isolated in Splunk from source `10.10.10.30` targeting `testuser1`. Unrelated Type 2/loopback failures were separated as local-console noise.

## Investigation Questions
- What account(s) are being targeted?
- Which source host/IP is generating the failures?
- Is there a success event after the failures?
- Did the activity result in a lockout, privilege use, or lateral movement attempt?
- Does the activity match expected lab testing or something unexpected?

## Validated Findings So Far

- Scope: one controlled source (`WEC01`) and one target (`TEST-WIN10-LAN1`)
- Target account: `testuser1`
- Pattern: 30 Type 3 failures from `10.10.10.30`
- Telemetry: validated locally, at WEC01, and in Splunk after repairing a Security-channel WEF access-denied condition
- Detection: generic per-account/per-source threshold logic validated in fixed five-minute buckets and saved as a private Splunk report
- Automation limitation: Splunk Free does not provide scheduled alerts; no automated alert deployment is claimed
- Outcome and final disposition: still under review; successful-logon correlation, final timeline, ATT&CK mapping, recommendations, and incident report remain

## Conclusion (To fill in later)
Write a short conclusion statement:
- What happened?
- How you know (key event IDs + pivots)
- What you’d improve (detection/hardening)

## Evidence Checklist
Add screenshots to `screenshots/` (redacted as needed):
- [x] Initial failed logon spike (platform view)
- [x] Pivot showing top source + top targeted user
- [ ] Any successful logon (if present) and context around it
- [ ] Account lockout evidence (if present)
- [ ] Final supporting screenshot that confirms the conclusion

## Files in this case
- `timeline.md` — ordered event sequence with timestamps
- `iocs.md` — artifacts collected (sanitized)
- `queries.md` — investigation pivots (Splunk/Elastic/Wazuh)
- `screenshots/` — redacted evidence
