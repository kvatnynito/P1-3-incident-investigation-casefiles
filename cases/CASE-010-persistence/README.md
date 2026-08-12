# CASE-010: Persistence Investigation

**Status:** Planned / not validated
**Curriculum position:** Lab 09 — Intermediate

## Objective

Detect, explain, classify, remove, and verify removal of a benign persistence mechanism while correlating its creation to the responsible user and process.

## Prerequisites

- Searchable scheduled-task or registry telemetry, process events, and authentication events
- A benign program/script and reversible lab-only persistence mechanism
- Recorded baseline and rollback procedure

## Ordered Steps

1. Create a benign persistence mechanism such as a scheduled task or startup entry.
2. Detect the newly created persistence mechanism.
3. Identify the user and process that created it.
4. Determine what program/script will execute and when.
5. Correlate registry, scheduled-task, process, and authentication telemetry.
6. Determine whether the persistence mechanism is legitimate.
7. Map it to MITRE ATT&CK.
8. Remove it and verify that persistence is gone.
9. Document the investigation and remediation.

## Completion Evidence

- Baseline, creation telemetry, creator/process, trigger, and payload description
- Correlated timeline and supported disposition
- ATT&CK mapping plus removal and post-removal verification

## Safety

Use a harmless program and a reversible mechanism. Record removal steps before creating persistence.

