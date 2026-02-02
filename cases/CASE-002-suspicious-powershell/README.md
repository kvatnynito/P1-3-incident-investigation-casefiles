# CASE-002: Suspicious PowerShell Execution
Status: Draft (to be updated during implementation)

## Scenario Summary
This case simulates suspicious PowerShell activity on a Windows endpoint and documents the investigation workflow from initial signal to conclusion.

## Why I’m doing this case
- Practice identifying suspicious command execution and common PowerShell abuse patterns
- Validate that endpoint telemetry is captured end-to-end (WEF/Sysmon + platforms)
- Build a clean timeline from process creation and related artifacts

## Lab Context (Representative)
- Source (operator/attacker): TBD (optional)
- Target endpoint: TBD (e.g., AD-WIN10 / AD-WIN11)
- Execution method: TBD (interactive / scheduled task / remote exec)

> Note: Hostnames/IPs in this case may be modified for safety.

## Starting Signal (What triggered the investigation)
TBD during implementation. Examples:
- PowerShell process creation (Sysmon Event ID 1)
- Suspicious command-line indicators (encoded command, download cradle)
- Unusual parent process (Office → PowerShell, WMI → PowerShell)

## Investigation Questions
- Which host and user ran PowerShell?
- What was the command line?
- What was the parent process?
- Did PowerShell spawn child processes?
- Was there network activity or file writes associated with it?

## Findings (To fill in later)
- Scope: TBD
- Time window: TBD
- User/context: TBD
- Command line highlights: TBD
- Outcome: TBD (benign admin action vs suspicious)

## Conclusion (To fill in later)
Write a short conclusion statement:
- What happened?
- How you know (key events + pivots)
- What you’d improve (detection/hardening)

## Evidence Checklist
Add screenshots to `screenshots/` (redacted as needed):
- [ ] Initial PowerShell event(s)
- [ ] Parent/child process relationship
- [ ] Command line details (sanitized as needed)
- [ ] Any related network or file artifacts (if present)
- [ ] Final supporting screenshot that confirms the conclusion

## Files in this case
- `timeline.md` — ordered event sequence with timestamps
- `iocs.md` — artifacts collected (sanitized)
- `queries.md` — Splunk/Elastic/Wazuh pivots used
- `screenshots/` — redacted evidence
