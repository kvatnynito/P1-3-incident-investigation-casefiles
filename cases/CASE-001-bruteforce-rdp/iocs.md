# Artifacts / IOCs — CASE-001 Brute Force / RDP
Status: Draft (to be updated during implementation)

> Sanitization note: Replace real internal IPs/usernames with representative values if needed.

## Accounts
- Targeted account(s): TBD
- Account type: TBD (domain / local)
- Lockout observed: TBD (yes/no)

## Hosts
- Source host (attacker): TBD
- Target host: TBD
- Collector (if referenced): TBD

## Network
- Source IP(s): TBD
- Destination IP/host: TBD
- Ports (if relevant): TBD (e.g., 3389 for RDP)

## Key Event Types Observed
- Windows Security:
  - 4625 (failed logon)
  - 4624 (successful logon) — if observed
  - 4740 (account locked out) — if observed
  - 4768/4769/4776 (auth-related) — if observed
- Sysmon (optional correlation):
  - 3 (network connection)
  - 1 (process creation) — if tooling used on target after success

## Notes
- Any unusual patterns (time of day, volume, spread across hosts)
- Any evidence of follow-on activity (process creation, new services, scheduled tasks)
