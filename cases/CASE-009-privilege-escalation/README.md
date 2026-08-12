# CASE-009: Privilege Escalation Investigation

**Status:** Planned / not validated
**Curriculum position:** Lab 08 — Intermediate

## Objective

Investigate an approved elevation of a standard lab account and distinguish legitimate administration from suspicious privilege change or use.

## Prerequisites

- Disposable standard and administrative lab accounts
- Searchable account, group-membership, process, and logon telemetry
- Documented rollback for any membership or privilege change

## Ordered Steps

1. Create a controlled scenario where a standard lab account obtains an approved elevated privilege.
2. Detect the privilege-related activity.
3. Identify the account, system, command/process, and privilege change.
4. Determine how elevation occurred.
5. Review surrounding logon and process activity.
6. Determine whether the elevation was authorized or suspicious.
7. Map the activity to MITRE ATT&CK.
8. Document the security impact and remediation.

## Completion Evidence

- Before/after privilege state and responsible actor/process
- Correlated logon and process timeline
- Authorization assessment, ATT&CK mapping, impact, rollback, and remediation

## Safety

Use disposable lab accounts and a reversible change. Do not weaken or alter the Fedora host or Proxmox administrative access.

