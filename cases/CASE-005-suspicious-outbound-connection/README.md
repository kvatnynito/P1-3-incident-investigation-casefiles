# CASE-005: Suspicious Outbound Network Connection

**Status:** Planned / not validated
**Curriculum position:** Lab 04 — Beginner

## Objective

Tie endpoint telemetry to network behavior by identifying the process responsible for an unusual outbound connection and deciding whether the connection is expected.

## Prerequisites

- Sysmon network-connection telemetry or equivalent endpoint evidence
- Splunk and, when useful, pfSense or packet-capture visibility
- A harmless lab-controlled destination

## Ordered Steps

1. Generate an unusual but harmless outbound connection from a Windows system.
2. Detect it using Sysmon, firewall logs, Splunk telemetry, or packet capture.
3. Identify the source host, destination IP, port, and protocol.
4. Identify the process responsible for the connection.
5. Correlate DNS activity and packet/network evidence.
6. Determine whether the connection is expected or anomalous.
7. Map the behavior to MITRE ATT&CK when appropriate.
8. Document the findings and recommended response.

## Completion Evidence

- Source/destination/port/protocol and responsible process
- DNS or packet evidence correlated to the same time window
- Supported disposition, timeline, ATT&CK mapping where applicable, and response recommendation

## Safety

Connect only to an owned lab service or another harmless destination approved for testing.

