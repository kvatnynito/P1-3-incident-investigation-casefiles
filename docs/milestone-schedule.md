# Milestone Schedule

## Project Status

P1-3 is currently in the planning / blueprint stage.

The case folders already exist, but the investigations are not complete yet.

P1-3 should not move into full case execution until P1-2 has validated the telemetry required for each case.

P1-3 does not document how telemetry was installed or configured. That work belongs in P1-2.

P1-3 documents how validated telemetry is used to investigate simulated security activity.

---

## Project Dependency Chain

Portfolio 1 is structured as a three-repo chain:

- P1-1 — Lab Infrastructure Foundation
- P1-2 — Telemetry Pipeline
- P1-3 — Incident Investigation Case Files

P1-3 depends on:

- segmented lab zones from P1-1
- validated log ingestion from P1-2
- documented telemetry sources from P1-2
- screenshots, searches, and validation evidence from P1-2 where relevant

P1-3 should not duplicate P1-2 setup documentation.

P1-3 should reference P1-2 as the telemetry source of truth.

---

## Documentation Boundary

### Belongs in P1-2

- Installing Splunk, Wazuh, Elastic, Sysmon, WEF, agents, or forwarders
- Configuring log forwarding
- Configuring collectors
- Proving logs arrive in SIEM/log platforms
- Documenting indexes, sourcetypes, agents, and ingestion paths
- Troubleshooting missing telemetry
- Validating platform ingestion

### Belongs in P1-3

- Choosing an investigation scenario
- Defining ground truth
- Searching validated telemetry
- Building a timeline
- Documenting evidence
- Writing analyst findings
- Identifying visibility gaps
- Creating detection improvement notes
- Writing lessons learned from the investigation

---

## Existing Planned Case Folders

The repository already contains the following planned case folders:

| Case | Folder | Current Status |
|---|---|---|
| CASE-001 | `cases/CASE-001-bruteforce-rdp/` | Planned / Not validated |
| CASE-002 | `cases/CASE-002-suspicious-powershell/` | Planned / Not validated |
| CASE-003 | `cases/CASE-003-web-attack-dvwa/` | Planned / Not validated |

These folders may contain templates or planning files, but a case is not complete until evidence, timeline, queries, screenshots/references, and analyst conclusions are documented.

---

## Milestone 1 — CASE-001 Brute Force RDP Investigation

### Goal

Investigate a simulated RDP brute-force scenario using validated Windows authentication telemetry.

### Status

Planned / Not validated

### Case Folder

`cases/CASE-001-bruteforce-rdp/`

### Depends On P1-2

This case should not begin until P1-2 has validated:

- Windows authentication logs
- failed logon events
- successful logon events
- source host or source IP visibility
- destination host visibility
- Splunk, Wazuh, or Elastic searchability

### Case Objectives

- Identify failed RDP logon activity
- Determine whether a successful logon followed the failures
- Identify source and destination systems
- Identify the account involved
- Build a timestamped event timeline
- Determine what the evidence supports
- Document what cannot be confirmed
- Identify detection or logging improvements

### Expected Case Files

- `cases/CASE-001-bruteforce-rdp/README.md`
- `cases/CASE-001-bruteforce-rdp/timeline.md`
- `cases/CASE-001-bruteforce-rdp/queries.md`
- `cases/CASE-001-bruteforce-rdp/iocs.md`
- `cases/CASE-001-bruteforce-rdp/screenshots.md`

### Expected Platform Notes

- `detections/splunk/case-searches.md`
- `detections/splunk/validation-searches.md`
- `detections/elastic/case-queries.md`
- `detections/elastic/validation-queries.md`
- `detections/wazuh/case-notes.md`
- `detections/wazuh/validation-notes.md`

### Expected Evidence

- failed logon events
- successful logon event if applicable
- source IP or host
- destination host
- username
- timestamps
- Splunk/Wazuh/Elastic searches
- screenshots or evidence references

### Completion Criteria

This case is complete only when:

- ground truth is documented
- telemetry source is identified
- queries are documented
- timeline is complete
- evidence is referenced
- conclusion is supported by evidence
- gaps and lessons learned are documented
- screenshot references exist where appropriate

---

## Milestone 2 — CASE-002 Suspicious PowerShell Investigation

### Goal

Investigate suspicious PowerShell activity using validated Windows and Sysmon telemetry.

### Status

Planned / Not validated

### Case Folder

`cases/CASE-002-suspicious-powershell/`

### Depends On P1-2

This case should not begin until P1-2 has validated:

- Sysmon deployment
- Sysmon process creation events
- Windows process or PowerShell-related logging
- user context
- host context
- Splunk, Wazuh, or Elastic searchability

### Case Objectives

- Identify PowerShell execution
- Review command line activity
- Identify parent process
- Identify user context
- Identify host context
- Determine whether the behavior appears expected or suspicious
- Build a timeline
- Document evidence and gaps
- Identify detection or hardening improvements

### Expected Case Files

- `cases/CASE-002-suspicious-powershell/README.md`
- `cases/CASE-002-suspicious-powershell/timeline.md`
- `cases/CASE-002-suspicious-powershell/queries.md`
- `cases/CASE-002-suspicious-powershell/iocs.md`
- `cases/CASE-002-suspicious-powershell/screenshots.md`

### Expected Platform Notes

- `detections/splunk/case-searches.md`
- `detections/splunk/validation-searches.md`
- `detections/elastic/case-queries.md`
- `detections/elastic/validation-queries.md`
- `detections/wazuh/case-notes.md`
- `detections/wazuh/validation-notes.md`

### Expected Evidence

- Sysmon process creation event
- PowerShell command line
- parent process
- username
- hostname
- timestamp sequence
- related Windows events if available
- Splunk/Wazuh/Elastic searches
- screenshots or evidence references

### Completion Criteria

This case is complete only when:

- ground truth is documented
- PowerShell telemetry is validated
- queries are documented
- timeline is complete
- evidence is referenced
- analyst conclusion is supported
- gaps and lessons learned are documented
- screenshot references exist where appropriate

---

## Milestone 3 — CASE-003 DVWA Web Attack Investigation

### Goal

Investigate a simulated web attack against DVWA using validated web, firewall, and platform telemetry.

### Status

Planned / Not validated

### Case Folder

`cases/CASE-003-web-attack-dvwa/`

### Depends On P1-2

This case should not begin until P1-2 has validated:

- DVWA host deployment
- relevant web or application logs if available
- firewall logs from pfSense
- attacker host visibility
- target host visibility
- Splunk, Wazuh, or Elastic searchability

### Case Objectives

- Identify attacker and target systems
- Identify web activity related to the scenario
- Review firewall or web logs
- Build a timeline of requests or alerts
- Determine what the evidence supports
- Document visibility gaps
- Identify detection or logging improvements

### Expected Case Files

- `cases/CASE-003-web-attack-dvwa/README.md`
- `cases/CASE-003-web-attack-dvwa/timeline.md`
- `cases/CASE-003-web-attack-dvwa/queries.md`
- `cases/CASE-003-web-attack-dvwa/iocs.md`
- `cases/CASE-003-web-attack-dvwa/screenshots.md`

### Expected Platform Notes

- `detections/splunk/case-searches.md`
- `detections/splunk/validation-searches.md`
- `detections/elastic/case-queries.md`
- `detections/elastic/validation-queries.md`
- `detections/wazuh/case-notes.md`
- `detections/wazuh/validation-notes.md`

### Expected Evidence

- attacker IP or host
- target IP or host
- web request evidence
- firewall logs
- timestamps
- HTTP method, URI, status code, or payload evidence if available
- Splunk/Wazuh/Elastic searches
- screenshots or evidence references

### Completion Criteria

This case is complete only when:

- ground truth is documented
- web or firewall telemetry is validated
- queries are documented
- timeline is complete
- evidence is referenced
- conclusion is supported
- gaps and lessons learned are documented
- screenshot references exist where appropriate

---

## Milestone 4 — Cross-Platform Investigation Validation

### Goal

Compare how investigation evidence appears across Splunk, Wazuh, and Elastic.

### Status

Planned / Not validated

### Depends On P1-2

This milestone should not begin until the relevant telemetry source is searchable in at least two platforms.

### Objectives

- Compare search workflow across platforms
- Document what each platform shows clearly
- Document what each platform misses or makes harder to find
- Identify platform-specific strengths and weaknesses
- Update detection/platform notes

### Expected Documentation

- `detections/splunk/case-searches.md`
- `detections/splunk/validation-searches.md`
- `detections/elastic/case-queries.md`
- `detections/elastic/validation-queries.md`
- `detections/wazuh/case-notes.md`
- `detections/wazuh/validation-notes.md`

### Completion Criteria

This milestone is complete only when:

- at least one case has evidence reviewed in more than one platform
- platform-specific searches or notes are documented
- differences between platforms are explained
- evidence references are included

---

## Milestone 5 — Detection Improvement Notes

### Goal

Turn investigation findings into detection ideas, logging gap notes, and hardening recommendations.

### Status

Planned / Not validated

### Objectives

- Identify what would have made the investigation easier
- Identify useful detection opportunities
- Identify noisy or weak signals
- Document possible tuning ideas
- Document logging gaps
- Document hardening or response recommendations

### Completion Criteria

This milestone is complete only when:

- at least one case has been completed
- detection ideas are tied to actual case evidence
- logging gaps are documented
- improvement notes are realistic and not overclaimed

---

## Milestone 6 — Final Portfolio Review

### Goal

Perform a final reviewer-focused cleanup after the investigation cases are complete.

### Status

Planned / Not validated

### Objectives

- Confirm README accurately reflects completed work
- Confirm case statuses are accurate
- Confirm screenshots and evidence references work
- Confirm no planned work is described as complete
- Confirm sensitive information is sanitized
- Confirm P1-1, P1-2, and P1-3 links are accurate
- Confirm commit history and documentation tell a clear project story

### Completion Criteria

This milestone is complete only when:

- completed cases have evidence
- planned cases are clearly labeled
- no overclaiming remains
- repo is safe for public review
- portfolio hub links are correct

---

## Current Next Step

Remain planned until P1-2 validates the telemetry needed for CASE-001.

P1-3 should stay planned until investigation evidence exists.

The first likely active case should be:

`CASE-001-bruteforce-rdp`

Reason:

- it can build from Windows authentication telemetry once P1-2 validates Windows log ingestion
- it teaches core SOC skills: failed logon review, successful logon review, account pivoting, host pivoting, timeline building, and evidence-based conclusions
