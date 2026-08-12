# CASE-008: Suspicious File / Malware Simulation

**Status:** Planned / not validated
**Curriculum position:** Lab 07 — Intermediate

## Objective

Investigate a harmless suspicious-file artifact from detection through scoping, containment, eradication, and recovery without introducing real malware.

## Prerequisites

- Approved harmless test artifact, such as the standard EICAR test file where supported
- Searchable file/process telemetry and a reversible test plan
- Isolated owned lab endpoint

## Ordered Steps

1. Introduce a harmless test artifact or controlled suspicious file; never store or use real malware.
2. Detect the file or associated endpoint activity.
3. Collect the filename, path, hash, user, and host.
4. Identify the process that created or executed it.
5. Check for related processes, persistence, file modifications, and network connections.
6. Determine the scope of affected activity.
7. Map the behavior to MITRE ATT&CK.
8. Write an incident report covering containment, eradication, and recovery.

## Completion Evidence

- File metadata/hash and associated process evidence
- Scope searches for related activity
- Supported disposition, timeline, ATT&CK mapping, and verified cleanup

## Safety

Use no real malware, payload, or destructive sample. Do not commit the artifact itself to this public repository.

