# Lab Dependencies

## Purpose

This file tracks what P1-3 needs from P1-1 and P1-2 before each investigation case can be completed.

P1-3 does not document how the lab or telemetry pipeline was built.

That work belongs in:

- P1-1 — lab infrastructure foundation
- P1-2 — telemetry pipeline validation

P1-3 uses those completed foundations to investigate simulated security activity and write case files.

---

## Dependency Boundary

### P1-1 Provides

- segmented lab zones
- VM placement
- pfSense routing and firewall context
- LAN1 and LAN2 network separation
- baseline systems used in later telemetry and investigation work

### P1-2 Provides

- validated log ingestion
- Splunk telemetry validation
- Wazuh telemetry validation
- Elastic telemetry validation
- Sysmon visibility
- Windows Event Forwarding or Windows log forwarding
- pfSense/firewall log visibility
- documented log source map

### P1-3 Provides

- investigation scenarios
- ground truth
- queries and pivots
- timelines
- evidence references
- analyst conclusions
- detection improvement notes
- logging gap notes

---

## Case Dependency Matrix

| Case | Investigation Focus | Required P1-2 Telemetry | Status |
|---|---|---|---|
| CASE-001-bruteforce-rdp | RDP brute force and logon review | Windows authentication logs, failed logons, successful logons, source/destination visibility | Waiting on P1-2 |
| CASE-002-suspicious-powershell | Suspicious PowerShell execution | Sysmon process creation, command line logging, user/host context | Waiting on P1-2 |
| CASE-003-web-attack-dvwa | Web attack against DVWA | DVWA/web logs if available, pfSense firewall logs, attacker/target visibility | Waiting on P1-2 |

---

## CASE-001 — Brute Force RDP Dependencies

This case should not be marked complete until the following evidence is available:

- failed logon events
- successful logon event if applicable
- username
- target host
- source host or source IP
- timestamp sequence
- searchable telemetry in Splunk, Wazuh, or Elastic
- screenshots or evidence references

Primary dependency:

- P1-2 Windows authentication telemetry validation

---

## CASE-002 — Suspicious PowerShell Dependencies

This case should not be marked complete until the following evidence is available:

- PowerShell process execution
- command line details
- parent process
- username
- hostname
- timestamp sequence
- Sysmon process creation event if available
- searchable telemetry in Splunk, Wazuh, or Elastic
- screenshots or evidence references

Primary dependency:

- P1-2 Sysmon and process telemetry validation

---

## CASE-003 — DVWA Web Attack Dependencies

This case should not be marked complete until the following evidence is available:

- attacker host or IP
- target host or IP
- web request evidence
- timestamps
- firewall logs
- web/application logs if available
- searchable telemetry in Splunk, Wazuh, or Elastic
- screenshots or evidence references

Primary dependency:

- P1-2 web/firewall telemetry validation

---

## Platform Decision

The primary platform for screenshots does not need to be decided yet.

Use this rule when case work begins:

- Splunk can be used as the primary case screenshot platform if it has the clearest searchable evidence.
- Wazuh can be used when host/security alert context is clearer there.
- Elastic can be used when timeline/search visualization is clearer there.

Do not force every case to use every platform.

Multi-platform comparison belongs later, after the first case has enough evidence.

---

## Current Dependency Status

| Dependency | Status |
|---|---|
| P1-1 segmented lab foundation | Complete |
| P1-2 Splunk ingestion | Planned / in progress |
| P1-2 Windows authentication telemetry | Not yet validated |
| P1-2 Sysmon telemetry | Not yet validated |
| P1-2 WEF or Windows log forwarding | Not yet validated |
| P1-2 Wazuh ingestion | Not yet validated |
| P1-2 Elastic ingestion | Not yet validated |
| P1-2 DVWA/web telemetry | Not yet validated |

---

## Rule

If a case depends on telemetry that has not been validated in P1-2, the case must stay:

- Planned
- Blocked
- Not validated

Do not mark a P1-3 case complete just because the folder exists.
