# CASE-004: Suspicious DNS Activity

**Status:** Planned / not validated
**Curriculum position:** Lab 03 — Beginner

## Objective

Investigate abnormal DNS activity from a Windows endpoint and correlate the queries to the responsible process without assuming unusual traffic is automatically malicious.

## Prerequisites

- Windows DNS-query telemetry searchable in Splunk (Sysmon Event ID 22 or equivalent)
- A controlled Windows endpoint and a documented activity window
- Optional DNS/firewall or packet-capture evidence for comparison

## Ordered Steps

1. Generate abnormal but harmless DNS traffic from a Windows endpoint.
2. Detect the unusual DNS queries.
3. Identify the endpoint, user, queried domains, and DNS server.
4. Examine query frequency, timing, record types, and responses.
5. Correlate the DNS activity with the process that generated it.
6. Determine whether it resembles normal application behavior, beaconing, tunneling, or another anomaly.
7. Map the relevant behavior to MITRE ATT&CK.
8. Write the findings and response recommendation.

## Completion Evidence

- Query results showing the DNS pattern and exact time window
- Process-to-domain correlation
- Timeline, artifacts, disposition, ATT&CK mapping, limitations, and response recommendation

## Safety

Use harmless domains or a lab-controlled DNS destination. Do not contact known malicious infrastructure.

