# Artifacts / IOCs — CASE-001 Brute Force / RDP
Status: Scope, threshold detection, and outcome check all validated. Findings/disposition/ATT&CK mapping remain.

> Sanitization note: values below are lab-internal RFC1918 addresses and a disposable local test account, safe to publish as-is.

## Accounts
- Targeted account: `testuser1` — disposable local account created specifically for this simulation
- Account type: Local (not domain) — created directly on `TEST-WIN10-LAN1`
- Lockout observed: **No.** Confirmed by live Splunk search (`EventCode=4740`, `Account_Name=testuser1`, All time) — 0 events. Consistent with the pre-check-confirmed `Never` local lockout policy, now backed by log evidence rather than policy assumption alone.

## Hosts
- Source host (controlled test source): `WEC01` (`10.10.10.30`)
- Target host: `TEST-WIN10-LAN1` (`10.10.10.100`)
- Collector: `WEC01` (also the source in this exercise — it received the RDP attempts and forwarded the resulting Windows Event Forwarding subscription data to Splunk)

## Network
- Source IP: `10.10.10.30`
- Destination IP/host: `10.10.10.100` / `TEST-WIN10-LAN1`
- Port: 3389 (RDP), authenticated via NLA — recorded as Logon Type 3 (Network), not Type 10 (RemoteInteractive)

## Key Event Types Observed
- Windows Security:
  - 4625 (failed logon) — confirmed, 30 events, Logon Type 3, `testuser1`, source `10.10.10.30`
  - 4624 (successful logon) — confirmed absent. `host=wec01 LogName=Security EventCode=4624 Account_Name=testuser1`, All time: 0 events. The brute-force attempt never succeeded.
  - 4740 (account locked out) — confirmed absent. `host=wec01 LogName=Security EventCode=4740 Account_Name=testuser1`, All time: 0 events.
  - 4768/4769/4776 — not checked; local account authentication on a workgroup-style local logon does not route through Kerberos, so these are not expected to apply here
- Sysmon (optional correlation):
  - Confirmed flowing for this host generally (10,000+ events during the same window). Follow-on correlation was not pursued further since no successful logon occurred — there is no post-compromise activity to correlate against.

## Notes
- Volume: 30 total failed attempts, clustered into three 5-minute buckets of 13, 8, and 5 — a manual/scripted burst pattern, not a slow low-and-slow spray
- Single source, single target, single account — no spread across multiple hosts or accounts observed
- Follow-on activity: not applicable — no successful logon occurred, so there is no post-authentication activity to check for
- Outcome: attempted, contained, no compromise. Every attempt in the 30-event burst failed; no account lockout resulted (attacker got 30 free guesses due to the `Never` lockout policy — see Lessons Learned / hardening recommendations in the incident report)
