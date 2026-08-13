# P1-3 Investigation Lab Plan

## Goal

Complete ten progressively harder, evidence-backed security-operations labs using the telemetry built in P1-2. Each lab is a separate public case file, while this document is the master checklist and execution order.

The recurring analyst workflow is:

> Generate activity → detect → identify → correlate → determine what happened → classify → respond → document

Generating an event is not completion. A lab is complete only when the observed evidence supports the findings, disposition, and recommended response.

## How the Labs Are Organized

The original P1-3 cases are preserved. Lab numbers describe the learning sequence; case numbers are stable public identifiers. `CASE-003-web-attack-dvwa` remains part of P1-3 but is outside this ten-lab CySA+-aligned sequence.

| Lab | Case folder | Difficulty | Primary skill | Status |
|---|---|---|---|---|
| 01 | `CASE-001-bruteforce-rdp` | Beginner | Failed-logon/password-guessing investigation | Complete — coached, not replication-verified |
| 02 | `CASE-002-suspicious-powershell` | Beginner | Process and PowerShell investigation | Planned |
| 03 | `CASE-004-suspicious-dns` | Beginner | DNS anomaly investigation | Planned |
| 04 | `CASE-005-suspicious-outbound-connection` | Beginner | Endpoint-to-network correlation | Planned |
| 05 | `CASE-006-bruteforce-vs-password-spray` | Intermediate | Authentication-pattern differentiation | Planned |
| 06 | `CASE-007-vulnerability-management` | Intermediate | Risk-based remediation workflow | Planned |
| 07 | `CASE-008-suspicious-file-simulation` | Intermediate | File/process scope investigation | Planned |
| 08 | `CASE-009-privilege-escalation` | Intermediate | Privilege-change investigation | Planned |
| 09 | `CASE-010-persistence` | Intermediate | Persistence detection and removal | Planned |
| 10 | `CASE-011-lateral-movement` | Advanced | Multi-host incident reconstruction | Planned |

## Sequencing Rules

1. Complete Labs 01–04 first to learn individual log sources and basic pivots.
2. Complete Labs 05–09 after basic searches, timelines, and dispositions feel comfortable.
3. Complete Lab 10 last because it requires correlating authentication, network, and process evidence across multiple Windows systems.
4. Use Splunk first because the P1-2 Windows → WEF → Splunk path is validated. Wazuh and Elastic comparisons remain optional until those platforms are actually built and validated.
5. Keep rough searches, unsanitized observations, and attack-generation details in the private `soc-detection-practice` companion. Promote only sanitized, evidence-backed conclusions here.
6. Before each live lab, verify the required VMs are deployed, powered on, and producing the required telemetry.

## Common Completion Gate

Every investigation must contain:

- [ ] documented scenario and ground truth
- [ ] exact activity window and systems/accounts involved
- [ ] confirmed telemetry source and search platform
- [ ] queries that returned the expected real lab evidence
- [ ] correlation across relevant user, host, process, file, DNS, and network fields
- [ ] timestamped timeline
- [ ] supported disposition: benign, suspicious, malicious, or needs more data
- [ ] MITRE ATT&CK mapping when applicable
- [ ] completed incident report using `docs/incident-report-template.md`
- [ ] recommended containment, remediation, escalation, or hardening action
- [ ] false-positive or limitation notes
- [ ] sanitized evidence references
- [ ] lessons learned and one detection/visibility improvement

## Lab 01 — Failed Logins / Password Guessing

Case: `cases/CASE-001-bruteforce-rdp/`

1. Generate repeated failed logins against several Windows accounts in the owned lab.
2. Find the authentication anomaly in Splunk.
3. Identify the source IP/host and targeted accounts.
4. Determine whether any authentication attempts succeeded.
5. Correlate the activity with Windows Security logs and endpoint telemetry.
6. Build and validate a detection query for the behavior.
7. Map the activity to MITRE ATT&CK.
8. Write a short incident report with findings and containment recommendations.

## Lab 02 — Suspicious PowerShell

Case: `cases/CASE-002-suspicious-powershell/`

1. Generate controlled, harmless suspicious-looking PowerShell activity.
2. Find the PowerShell execution in the logs.
3. Identify the user, hostname, command line, and parent process.
4. Determine what the command attempted to do.
5. Check for related file changes, child processes, or outbound connections.
6. Classify the behavior as benign, suspicious, malicious, or needs more data.
7. Map the activity to MITRE ATT&CK.
8. Document the investigation and recommended response.

## Lab 03 — Suspicious DNS Activity

Case: `cases/CASE-004-suspicious-dns/`

1. Generate abnormal but harmless DNS traffic from a Windows endpoint.
2. Detect the unusual DNS queries.
3. Identify the endpoint, user, queried domains, and DNS server.
4. Examine query frequency, timing, record types, and responses.
5. Correlate the DNS activity with the process that generated it.
6. Determine whether it resembles normal application behavior, beaconing, tunneling, or another anomaly.
7. Map the relevant behavior to MITRE ATT&CK.
8. Write the findings and response recommendation.

## Lab 04 — Suspicious Outbound Network Connection

Case: `cases/CASE-005-suspicious-outbound-connection/`

1. Generate an unusual but harmless outbound connection from a Windows system.
2. Detect it using Sysmon, firewall logs, Splunk telemetry, or packet capture.
3. Identify the source host, destination IP, port, and protocol.
4. Identify the process responsible for the connection.
5. Correlate DNS activity and packet/network evidence.
6. Determine whether the connection is expected or anomalous.
7. Map the behavior to MITRE ATT&CK when appropriate.
8. Document the findings and recommended response.

## Lab 05 — Brute Force vs. Password Spraying

Case: `cases/CASE-006-bruteforce-vs-password-spray/`

1. Generate one scenario using many passwords against one account and another using one/few passwords against many accounts.
2. Find both authentication patterns in Splunk.
3. Identify the targeted accounts and source systems.
4. Compare timing, volume, and account distribution.
5. Determine which scenario is brute force and which is password spraying.
6. Check whether either resulted in successful authentication.
7. Create and validate detection logic that distinguishes the two.
8. Document the reasoning and MITRE ATT&CK mapping.

## Lab 06 — Vulnerability Management

Case: `cases/CASE-007-vulnerability-management/`

1. Run a vulnerability scan against explicitly scoped lab systems.
2. Review and rank the findings.
3. Eliminate obvious false positives or irrelevant findings.
4. Validate one or more important findings manually using safe, read-only checks where practical.
5. Prioritize remediation by severity, exploitability, exposure, and asset importance.
6. Apply the remediation after recording its effect and rollback procedure.
7. Rescan to verify the issue is fixed.
8. Write a vulnerability assessment showing before → remediation → after.

## Lab 07 — Suspicious File / Malware Simulation

Case: `cases/CASE-008-suspicious-file-simulation/`

1. Introduce a harmless test artifact or controlled suspicious file; never store or use real malware.
2. Detect the file or associated endpoint activity.
3. Collect the filename, path, hash, user, and host.
4. Identify the process that created or executed it.
5. Check for related processes, persistence, file modifications, and network connections.
6. Determine the scope of affected activity.
7. Map the behavior to MITRE ATT&CK.
8. Write an incident report covering containment, eradication, and recovery.

## Lab 08 — Privilege Escalation Investigation

Case: `cases/CASE-009-privilege-escalation/`

1. Create a controlled scenario where a standard lab account obtains an approved elevated privilege.
2. Detect the privilege-related activity.
3. Identify the account, system, command/process, and privilege change.
4. Determine how elevation occurred.
5. Review surrounding logon and process activity.
6. Determine whether the elevation was authorized or suspicious.
7. Map the activity to MITRE ATT&CK.
8. Document the security impact and remediation.

## Lab 09 — Persistence Investigation

Case: `cases/CASE-010-persistence/`

1. Create a benign persistence mechanism such as a scheduled task or startup entry.
2. Detect the newly created persistence mechanism.
3. Identify the user and process that created it.
4. Determine what program/script will execute and when.
5. Correlate registry, scheduled-task, process, and authentication telemetry.
6. Determine whether the persistence mechanism is legitimate.
7. Map it to MITRE ATT&CK.
8. Remove it and verify that persistence is gone.
9. Document the investigation and remediation.

## Lab 10 — Lateral Movement

Case: `cases/CASE-011-lateral-movement/`

1. Simulate approved remote access between two lab Windows machines using SMB or RDP.
2. Detect the connection or authentication activity.
3. Identify the source machine, destination machine, and account used.
4. Determine whether authentication succeeded.
5. Correlate authentication, network, and process logs to reconstruct what happened.
6. Determine what resources or systems were accessed.
7. Map the activity to MITRE ATT&CK.
8. Document the attack path and recommended containment.

## Career Translation

Completing the sequence demonstrates more than familiarity with security tools. It produces defensible examples of authentication analysis, endpoint investigation, network correlation, detection logic, vulnerability prioritization, incident timelines, MITRE ATT&CK mapping, and written response recommendations—the work expected of an entry-level SOC or security analyst.
