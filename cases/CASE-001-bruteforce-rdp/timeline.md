# Timeline — CASE-001 Brute Force / RDP
Status: Evidence-backed through the outcome check. Findings/disposition/ATT&CK mapping/incident report remain.

## Time Normalization
- Timezone used in this case: local endpoint time (`TEST-WIN10-LAN1`'s own Security event log), e.g. the 30 failed-logon events land at approximately 9:40 AM local.
- **Known discrepancy, not yet resolved:** during ingestion troubleshooting, one raw forwarded event showed 09:34 AM in its own payload while Splunk's `Time` column displayed 4:34 PM for the same event — roughly a 7-hour offset (`case-evidence` screenshots, query-attempt03). This looks like a UTC-vs-local display difference between the endpoint/collector and Splunk's rendered time rather than a real clock-drift fault, but it has not been confirmed either way. Treat exact clock times below as approximate and endpoint-relative, not as Splunk-search-bar-relative, until this is resolved.

## Timeline

This case's evidence splits into two layers: **(A)** the scenario/attack activity itself, and **(B)** the investigation/detection-engineering activity that followed it (telemetry repair, scoping, detection build). Both are evidence-backed; (B) is unusually large here because this case's real teaching value ended up being telemetry repair, not just query-writing — see `docs/current-status.md` for the full troubleshooting record, not repeated here.

### (A) Scenario / attack activity

| Time | Host | Event Source | Event ID / Type | Summary | Notes / Pivot |
|---|---|---|---|---|---|
| Pre-activity | `TEST-WIN10-LAN1` | Local policy (`net accounts`) | n/a | Safety pre-check: local account-lockout threshold confirmed `Never` | Chosen specifically so repeated failures could be generated without locking the disposable test account |
| Pre-activity | `TEST-WIN10-LAN1` | n/a | n/a | Disposable local account `testuser1` created | Scoped to this exercise only, not a real user |
| Pre-activity | `TEST-WIN10-LAN1` | n/a | n/a | Remote Desktop enabled on target | Required before any RDP attempts could be generated at all |
| ~9:40 AM (endpoint-local) | `TEST-WIN10-LAN1` | Windows Security (local log) | 4625 ×30 | Failed RDP/NLA logon burst against `testuser1` from `10.10.10.30` (`WEC01`) | Logon Type 3 (Network — expected for NLA/CredSSP pre-auth failures on RDP, not Type 10 RemoteInteractive) |
| After the burst (live-checked 2026-08-12) | `TEST-WIN10-LAN1` | Windows Security | 4624 | **Confirmed absent.** No successful logon ever occurred for `testuser1` from `10.10.10.30` | `host=wec01 LogName=Security EventCode=4624 Account_Name=testuser1`, All time: 0 events (`case-evidence-splunk-4624-outcome-zero-results.png`) |
| After the burst (live-checked 2026-08-12) | `TEST-WIN10-LAN1` | Windows Security | 4740 | **Confirmed absent.** No account lockout occurred | `host=wec01 LogName=Security EventCode=4740 Account_Name=testuser1`, All time: 0 events (`case-evidence-splunk-4740-outcome-zero-results.png`) |
| n/a | `TEST-WIN10-LAN1` | Sysmon | 1 / 3 | Follow-on process creation or network connections | Not applicable — no successful logon occurred, so there is no post-authentication activity to correlate |

### (B) Investigation / detection-engineering activity

| Time | Host | Event Source | Event ID / Type | Summary | Notes / Pivot |
|---|---|---|---|---|---|
| Same session, after the burst | `TEST-WIN10-LAN1` | Eventlog-ForwardingPlugin | Warning 101 | Source-side WEF diagnostic isolates the fault: Sysmon `ErrorCode=0`, Security `ErrorCode=5` (access denied) | Explains why the 30 local 4625 events weren't yet visible at WEC01/Splunk |
| Same session, after ACL fix | `TEST-WIN10-LAN1` → `WEC01` | Windows Event Forwarding | 4625 | Genuine forwarded Security 4625 event confirmed arriving at WEC01 | Proves the WEF hop specifically, before checking Splunk |
| Same session, after ACL fix | `WEC01` → Splunk | Security (forwarded) | 4625 | Genuine forwarded Security 4625 events confirmed arriving in Splunk | Full pipeline (`TEST-WIN10-LAN1` → WEC01 → Splunk) validated end to end |
| Same session | Splunk | Security | 4625 | Events grouped by `Account_Name`, `Logon_Type`, `Source_Network_Address` | Separated the controlled Type 3 set from unrelated local Type 2/loopback console-logon noise |
| Same session | Splunk | Security | 4625 | 30 events isolated: `Logon_Type=3`, `Source_Network_Address=10.10.10.30` | Matches the local-log count exactly — confirms no forwarding loss |
| Same session | Splunk | Security | 4625 | Fixed 5-minute-bucket threshold search (`count>=5` per account/source) validated | Three qualifying buckets: 13, 8, 5 — detection logic does not hardcode the account or source |
| Same session | Splunk | n/a | n/a | Detection saved as private report `CASE-001 - Network Logon Failure Threshold` | Splunk Free has no scheduled alerting — saved/rerunnable report only, not an automated alert |

## Notes
- Logon Type 3 (Network) is expected here, not Type 10 (RemoteInteractive) — RDP with NLA pre-authenticates over Type 3 before the interactive session would establish.
- Failure reason/substatus codes have not yet been pulled from the raw events — worth adding if distinguishing "bad password" from other failure substatus codes becomes relevant to the findings.
- Source `10.10.10.30` is expected/known-controlled in this lab (`WEC01`, used deliberately as the attack-simulation source) — not an unexpected external IP.
- Outcome: the brute-force attempt was contained by outcome, not by policy — the account was never locked (30 free guesses were available under the `Never` lockout policy), but the attacker also never guessed the correct password. This is a real gap worth calling out in the incident report's hardening recommendations even though this specific attempt didn't exploit it.
