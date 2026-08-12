# Investigation Workflow

Use this workflow for every P1-3 case:

1. **Generate activity:** record the approved scenario and ground truth.
2. **Detect:** confirm the signal exists in a validated telemetry source.
3. **Identify:** record the relevant time range, user, host, process, source, and destination.
4. **Correlate:** pivot across authentication, endpoint, file, DNS, and network evidence as applicable.
5. **Determine:** reconstruct what actually happened and state what remains unknown.
6. **Classify:** choose a defensible disposition—benign, suspicious, malicious, or needs more data.
7. **Respond:** recommend containment, remediation, escalation, or hardening proportional to the evidence.
8. **Document:** preserve queries, a timeline, sanitized artifacts/evidence, limitations, ATT&CK mapping where applicable, and lessons learned.

The per-case numbered steps and common completion gate are in [`plan.md`](plan.md).
