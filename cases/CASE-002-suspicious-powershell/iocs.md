# Artifacts / IOCs — CASE-002 Suspicious PowerShell
Status: Draft (to be updated during implementation)

> Sanitization note: Replace real internal IPs/usernames/paths with representative values if needed.

## Accounts
- User executing PowerShell: TBD
- Account type: TBD (domain / local)
- Privilege context: TBD (standard user / admin)

## Hosts
- Target host: TBD (e.g., AD-WIN10 / AD-WIN11)
- Source host (if remote execution): TBD
- Collector (if referenced): TBD

## Process Artifacts
- Parent process: TBD (name + command line)
- Process: powershell.exe (or pwsh.exe) — TBD details
- Command line (high-level summary): TBD
- Child processes (if any): TBD
- Related tools/utilities observed (if any): TBD

## File Artifacts (if applicable)
- Files created/dropped: TBD (paths sanitized)
- Downloads written to disk: TBD
- Hashes (if captured): TBD

## Network Artifacts (if applicable)
- Destination host/IP: TBD (sanitized)
- Ports/protocols: TBD
- URLs/domains (if any): TBD (sanitize or replace with example.com)

## Key Event Types Observed (expected)
- Sysmon:
  - 1 (Process creation)
  - 3 (Network connection) — if observed
  - 11 (File create) — if observed
- Windows Security (optional, if enabled):
  - 4688 (Process creation)
  - 4624 (Logon) — if remote/interactive context matters

## Notes
- Suspicious indicators to document (if present):
  - Encoded commands
  - Download cradle patterns
  - Unusual parent process (Office/WMI/script host → PowerShell)
  - Unusual execution paths or hidden window flags
- Final determination: TBD (benign admin activity vs suspicious)
