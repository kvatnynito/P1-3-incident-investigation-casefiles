# CASE-011: Lateral Movement Investigation

**Status:** Planned / blocked on a second telemetry-ready Windows host
**Curriculum position:** Lab 10 — Advanced

## Objective

Reconstruct approved remote access between two Windows systems by correlating authentication, network, process, and resource-access evidence across both hosts.

## Prerequisites

- Two Windows systems with synchronized time and searchable telemetry
- Approved SMB or RDP path and a disposable lab account
- Source, destination, account, protocol, resource, and exact activity window recorded as ground truth
- Current inventory has only one fully telemetry-ready Windows endpoint; validate/build the second source before execution

## Ordered Steps

1. Simulate approved remote access between two lab Windows machines using SMB or RDP.
2. Detect the connection or authentication activity.
3. Identify the source machine, destination machine, and account used.
4. Determine whether authentication succeeded.
5. Correlate authentication, network, and process logs to reconstruct what happened.
6. Determine what resources or systems were accessed.
7. Map the activity to MITRE ATT&CK.
8. Document the attack path and recommended containment.

## Completion Evidence

- Evidence from both hosts and the relevant network path
- Supported multi-host timeline and authentication outcome
- Accessed-resource scope, ATT&CK mapping, containment recommendation, and identified visibility gaps

## Safety

Use only owned lab systems and approved credentials. Keep the simulation minimal and do not include offensive remote-execution procedures in the public case file.

