# P1-3: Incident Investigation Case Files (Attack Simulation + Triage)

## Overview
This repo contains **sanitized incident-style case files** generated from my homelab. Each case documents a complete workflow: simulate activity, confirm telemetry capture, investigate using platform queries, build a timeline, and record findings and improvements.

## Sanitization Note
This repo uses representative hostnames/IP ranges and redacts WAN/public IPs, domains/DDNS, VPN details, and secrets. The workflow is accurate, but specific identifiers may be modified.

## Why I’m building this
I wanted a structured way to practice the “end-to-end” cycle of security work:
- generating realistic signals in a controlled lab
- validating visibility across logging platforms
- turning raw events into a timeline and clear conclusions
- capturing lessons learned (detection tuning, hardening ideas, and rule improvements)

## Dependencies
These case files build on:
- `P1-1-proxmox-segmentation-lab` (segmentation + VM inventory)
- `P1-2-wef-sysmon-to-wazuh-elastic-splunk` (telemetry pipeline)

## Case File Format
Each case folder includes:
- `README.md` — summary of the scenario and what was observed
- `timeline.md` — timestamps and sequence of events
- `iocs.md` — artifacts (users/hosts/IPs/hashes), sanitized as needed
- `queries.md` — Splunk SPL / Elastic KQL / Wazuh pivots used
- `screenshots/` — redacted evidence

## Starter Cases (planned)
- CASE-001: Brute force → successful logon (Windows authentication focus)
- CASE-002: Suspicious PowerShell execution (endpoint behavior focus)
- CASE-003: Web attack against DVWA/WebGoat (web activity focus)

## Current Status
Blueprint stage. I’m creating templates firs
