https://github.com/kvatnynito/Cybersecurity-Portfolio1

# P1-3: Incident Investigation Case Files (Attack Simulation / Triage)

## Overview

This repo is planned to document **sanitized incident-style case files** generated from my homelab.

Each case is intended to follow a complete workflow: simulate activity, confirm telemetry capture, investigate using platform queries, build a timeline, and record findings, evidence, and improvements.

This project is the final repo in Portfolio 1 and is planned to build on the lab foundation and telemetry pipeline created in the first two repos.

---

## Status

**Current state:** Planned  
**Execution state:** Blueprint stage / not yet started  
**Prerequisites:** `P1-1-proxmox-segmentation-lab` and `P1-2-wef-sysmon-to-wazuh-elastic-splunk`

I’m preparing this repo in advance so the case structure, workflow, and starter scenarios are already defined before the first full investigation is built.

---

## Sanitization Note

This repo uses representative hostnames and IP ranges and redacts WAN/public IPs, domains/DDNS, VPN details, and secrets.

The workflow is intended to remain accurate, but specific identifiers may be modified for safety.

---

## Why I’m Building This

I wanted a structured way to practice the full end-to-end cycle of security work:

- generating realistic signals in a controlled lab
- validating visibility across logging platforms
- turning raw events into a timeline and clear conclusions
- capturing lessons learned such as detection tuning, hardening ideas, and rule improvements

As I’ve been learning security monitoring and incident response, I kept noticing the same patterns come up — failed logons, suspicious PowerShell, noisy web attacks, and “maybe this is nothing” events that still need a clean way to validate.

This repo is meant to be my way of practicing that in a controlled lab:

- create realistic activity on purpose so I know what the ground truth looks like
- confirm the telemetry is actually captured end-to-end
- investigate using consistent pivots such as user → host → process → network
- write down what happened, what evidence supports it, and what I would improve next time

---

## Dependencies

These planned case files are intended to build on:

- `P1-1-proxmox-segmentation-lab` for segmentation, VM placement, and network context
- `P1-2-wef-sysmon-to-wazuh-elastic-splunk` for telemetry collection, forwarding, and searchability

Without those earlier repos in place, this repo remains in blueprint stage.

---

## Planned Case File Format

Each future case folder is expected to include:

- `README.md` — summary of the scenario and what was observed
- `timeline.md` — timestamps and sequence of events
- `iocs.md` — artifacts such as users, hosts, IPs, and hashes, sanitized as needed
- `queries.md` — Splunk SPL, Elastic queries, Wazuh pivots, or other search logic used
- `screenshots/` — redacted evidence

---

## Planned Investigation Workflow

Once execution begins, the intended workflow for each case is:

### 1. Simulate or trigger activity
- generate realistic lab activity on purpose
- record the expected ground truth

### 2. Confirm telemetry capture
- verify the relevant events were captured through the pipeline
- confirm the activity is visible in the target platforms

### 3. Investigate the event
- pivot across host, user, process, and network activity
- identify the sequence of actions
- collect supporting evidence

### 4. Build a case file
- write the timeline
- record artifacts and queries used
- summarize findings and analyst conclusions

### 5. Capture follow-up improvements
- note detection tuning ideas
- identify logging gaps
- record hardening or response improvements

---

## Starter Cases (Planned)

- **CASE-001:** Brute force → successful logon  
  *Focus:* Windows authentication and logon visibility

- **CASE-002:** Suspicious PowerShell execution  
  *Focus:* endpoint behavior and process investigation

- **CASE-003:** Web attack against DVWA / WebGoat  
  *Focus:* web activity, attacker behavior, and event correlation

---

## Planned Deliverables

This repo is expected to eventually include:

- sanitized case folders
- timelines and investigation summaries
- IOC and artifact documentation
- platform-specific queries and pivots
- redacted evidence screenshots
- lessons learned and improvement notes tied to each case

---

## Planned Skill Areas

This project is intended to help build experience in:

- incident triage
- timeline creation
- multi-platform investigation
- evidence collection
- query-based pivoting
- translating raw telemetry into clear findings
- documenting case conclusions in a repeatable format

---

## Current Status

Blueprint stage.

At this point, I am defining the structure, templates, and starter cases so the repo is ready once the lab foundation and telemetry pipeline are in place.

---

## Planned Next Steps

When work begins on this repo, the initial implementation focus will likely be:

- finalize case templates
- choose the first simulated scenario
- confirm that required telemetry exists in the pipeline
- build the first complete investigation timeline
- store the first sanitized case file with supporting evidence

---

## License

MIT — see `LICENSE`.
