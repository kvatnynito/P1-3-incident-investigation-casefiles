# P1-3: Incident Investigation Case Files (Attack Simulation + Triage)

## Overview
This repo contains **sanitized incident-style case files** built from my homelab telemetry. Each case follows a repeatable workflow: generate activity, confirm logs are captured, investigate using queries, build a timeline, and document findings.

## Sanitization Note
This repo uses representative hostnames/IP ranges and redacts WAN/public IPs, domains/DDNS, VPN details, and secrets. The investigation workflow is accurate, but identifiers may be modified.

## Why I’m building this
I wanted a place to practice the part that matters in interviews:
- turning raw telemetry into an investigation story
- showing how I pivot from one event to the next
- documenting conclusions clearly (what happened, when, how I know)

## Dependencies
These cases assume:
- Lab segmentation + VM layout from `P1-1-proxmox-segmentation-lab`
- Telemetry pipeline from `P1-2-wef-sysmon-to-wazuh-elastic-splunk`

## Case File Format
Each case folder includes:
- `README.md` — summary + what I observed
- `timeline.md` — timestamps + sequence of events
- `iocs.md` — IPs/users/hosts/hashes (sanitized)
- `queries.md` — Splunk SPL / Elastic KQL / Wazuh pivots used
- `screenshots/` — redacted evidence

## Starter Cases (planned)
- CASE-001: Brute force → successful logon (Windows auth focus)
- CASE-002: Suspicious PowerShell execution (endpoint behavior focus)
- CASE-003: Web attack against DVWA/WebGoat (web telemetry focus)

## Current Status
Blueprint stage. I’m creating the case templates first, then generating evidence as I run each scenario in the lab.
