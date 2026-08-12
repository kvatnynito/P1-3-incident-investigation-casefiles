# CASE-006: Brute Force vs. Password Spraying

**Status:** Planned / not validated
**Curriculum position:** Lab 05 — Intermediate

## Objective

Distinguish two authentication-attack patterns using account distribution, password-attempt behavior, timing, volume, and outcomes rather than treating every failed-logon spike alike.

## Prerequisites

- Searchable Windows failed- and successful-logon events
- Multiple disposable lab accounts with lockout risk reviewed first
- A controlled source and exact ground-truth record for both scenarios

## Ordered Steps

1. Generate one scenario using many passwords against one account and another using one/few passwords against many accounts.
2. Find both authentication patterns in Splunk.
3. Identify the targeted accounts and source systems.
4. Compare timing, volume, and account distribution.
5. Determine which scenario is brute force and which is password spraying.
6. Check whether either resulted in successful authentication.
7. Create and validate detection logic that distinguishes the two.
8. Document the reasoning and MITRE ATT&CK mapping.

## Completion Evidence

- Side-by-side query results for both patterns
- Detection logic tested against both scenarios
- Success/failure outcome, reasoning, timeline, ATT&CK mapping, limitations, and recommendation

## Safety

Use only disposable lab accounts. Review account-lockout policy and recovery before generating activity; keep attempt counts minimal.

