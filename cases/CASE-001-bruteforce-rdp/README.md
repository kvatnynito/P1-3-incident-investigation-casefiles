# CASE-001: Failed Logins / Password Guessing Investigation

**Status:** Complete — evidence-backed investigation, detection, MITRE ATT&CK mapping, and disposition documented. The work was completed live with coaching and is not replication-verified.
**Curriculum position:** Lab 01 — Beginner

## Lab Context

### Ordered Steps
1. Generate repeated failed logins against a disposable Windows account in the owned lab.
2. Find the authentication anomaly in Splunk.
3. Identify the source IP/host and targeted accounts.
4. Determine whether any authentication attempts succeeded.
5. Correlate the activity with Windows Security logs and endpoint telemetry.
6. Build and validate a detection query for the behavior.
7. Map the activity to MITRE ATT&CK.
8. Write a short incident report with findings and containment recommendations.

### Safety
Use only disposable lab accounts. Review the account-lockout policy and recovery procedure before generating activity, and keep the attempt count minimal.

### Why I'm doing this case
- Practice identifying high-volume failed logon patterns
- Validate that authentication telemetry is captured end-to-end (WEF/Sysmon + platforms)
- Build a clean timeline from Windows security events and related context

### Lab Context (Representative)
- Source host (controlled test source): `WEC01` (`10.10.10.30`)
- Target host: `TEST-WIN10-LAN1`
- Account targeted: disposable local account `testuser1`
- Access path: RDP/NLA authentication, recorded as Security Event ID 4625 with Logon Type 3

> Note: Hostnames/IPs in this case may be modified for safety.

---

# Incident Report

Structured per `docs/incident-report-template.md`.

## Executive Summary

Between approximately 9:40 AM (endpoint-local time) on 2026-08-12, the disposable local account `testuser1` on `TEST-WIN10-LAN1` (`10.10.10.100`) received 30 failed RDP/NLA network-logon attempts (Windows Security Event ID 4625, Logon Type 3) from a single controlled source, `WEC01` (`10.10.10.30`), clustered into three bursts of 13, 8, and 5 within 5-minute windows. A live Splunk outcome check confirmed zero successful logons (Event ID 4624) and zero account lockouts (Event ID 4740) — the activity resulted in no compromise. This was an authorized, controlled simulation in an owned lab, not a real external attack.

## Scenario and Ground Truth

- **Approved activity generated:** 30 controlled failed RDP/NLA authentication attempts against a disposable local Windows account.
- **Source and destination:** `WEC01` (`10.10.10.30`) → `TEST-WIN10-LAN1` (`10.10.10.100`), port 3389 (RDP).
- **Account/user:** `testuser1` — disposable local account, created specifically for this exercise.
- **Exact start/end time:** ~9:40 AM, endpoint-local time (`TEST-WIN10-LAN1`'s own Security event log). A known, unresolved endpoint-vs-Splunk clock-display discrepancy (~7 hours) is documented in `timeline.md` — treat exact clock times as approximate and endpoint-relative.
- **Expected telemetry:** Windows Security Event ID 4625 (failed logon), Logon Type 3, forwarded via Windows Event Forwarding (WEF) through `WEC01` into Splunk.

## Initial Signal

- **Alert or search that started the investigation:** Manual Splunk search for `EventCode=4625` — this was a self-generated exercise, not a real production alert.
- **Platform and data source:** Splunk, sourced from the Windows Security event log via WEF/`WEC01`.
- **Detection status:** Started as a manual hunt; a validated, reusable threshold search now exists, saved as the private Splunk report `CASE-001 - Network Logon Failure Threshold`.

## Scope

| Field | Finding | Evidence reference |
|---|---|---|
| Time range | ~9:40 AM endpoint-local, three 5-minute bursts | `timeline.md` |
| Host(s) | Target: `TEST-WIN10-LAN1` (`10.10.10.100`); source: `WEC01` (`10.10.10.30`) | `iocs.md` |
| User/account(s) | `testuser1` (local, disposable) | `iocs.md` |
| Source/destination | `10.10.10.30` → `10.10.10.100`:3389 (RDP) | `iocs.md` |
| Process/file/domain | Not applicable — no successful logon occurred, so there is no post-authentication process/file/domain activity to scope | `iocs.md` |

## Searches and Correlation

Full query text, validated results, and tuning limitations live in `queries.md` and `detections/splunk/case-searches.md` — summarized here:

1. **Ingestion confirmation** (`EventCode=4625` on `wec01`) — confirmed genuine failed-logon events reaching Splunk, but only after diagnosing and repairing a real WEF telemetry gap first: the Security channel was silently failing to forward (`ErrorCode=5`, access denied) while Sysmon on the same subscription forwarded fine. Root cause and fix are documented in `docs/current-status.md` and the private SOP's Troubleshooting Entry 2.
2. **Scoping/grouping** (`stats count by Account_Name Logon_Type Source_Network_Address`) — separated the controlled Type 3 network-logon failures from unrelated local Type 2/loopback console noise, and confirmed no other account or source was involved.
3. **Isolation** (`Logon_Type=3 Source_Network_Address=10.10.10.30`) — isolated exactly 30 events, matching the local endpoint log count with no forwarding loss.
4. **Threshold detection** (fixed 5-minute `bin`, `count>=5` per account/source) — validated three qualifying buckets (13, 8, 5) without hardcoding the account or source.
5. **Outcome check** (`EventCode=4624` and `EventCode=4740`, scoped to `testuser1`) — both returned 0 events over All time, confirmed live in Splunk on 2026-08-12 (`case-evidence-splunk-4624-outcome-zero-results.png`, `case-evidence-splunk-4740-outcome-zero-results.png`).

**Telemetry gap found and fixed along the way:** the Security channel's WEF forwarding was broken by a channel-specific access-control gap, not a Splunk ingestion problem — see Detection and Visibility Improvements below.

## Timeline

Full evidence-backed timeline in `timeline.md`, split into (A) scenario activity and (B) investigation/detection-engineering activity. Summary: safety pre-check → disposable account created → RDP enabled → 30 failed logons generated locally (~9:40 AM) → telemetry gap discovered and repaired → genuine events confirmed at `WEC01` then Splunk → controlled set scoped and isolated → threshold detection validated and saved → live outcome check confirmed zero successes and zero lockouts.

## Findings

**Observed, evidence-backed facts:**
- 30 Windows Security Event ID 4625 (failed logon) events on `TEST-WIN10-LAN1`, all Logon Type 3 (Network — consistent with RDP/NLA pre-authentication), all targeting `testuser1`, all originating from `10.10.10.30`.
- The 30 events cluster into three tight bursts (13, 8, 5 within 5-minute buckets) rather than an even drip — a pattern more consistent with scripted/manual rapid-retry activity than a slow, detection-evading trickle.
- Zero successful logons (4624) for this account/source pair, confirmed by direct search over All time.
- Zero account lockouts (4740), confirmed by direct search over All time — not merely assumed from the pre-activity policy check.
- A real, separate finding: this entire event set was initially invisible in Splunk due to a Security-channel WEF forwarding failure (`ErrorCode=5`, access denied) unrelated to the attack itself. The activity was fully logged locally on the endpoint the whole time — the SIEM simply couldn't see it until the forwarding ACL was repaired. That's a detection-coverage finding in its own right, independent of this specific case's outcome.

**What did not happen (stated explicitly, not just implied by absence):**
- No credential compromise.
- No follow-on process activity, privilege escalation, or lateral movement — there is nothing to correlate, since no session was ever established.
- No denial-of-service side effect on the legitimate account via lockout.

**What remains genuinely unknown (analyst judgment, not evidence):**
- Whether the 30 attempts represent an actual malicious actor, an automated tool run against this address by design (this lab's own controlled activity), or some other explanation — in this specific case the answer is known out-of-band (it's the lab's own controlled simulation), but the Windows Security log alone cannot distinguish attacker-generated failures from, say, a legitimate user who forgot a recently changed password and mistyped it 30 times. This exact discernment problem is scoped as CASE-006 (bruteforce-vs-password-spray) in this project's curriculum.

## MITRE ATT&CK Mapping

| Tactic | Technique / sub-technique | Why the evidence supports it | Evidence reference |
|---|---|---|---|
| Credential Access | Brute Force: Password Guessing (`T1110.001`) | Splunk showed repeated Security Event ID 4625 failures from one source against one account, `testuser1`. The account/source grouping query established multiple failed guesses against that single account, making Password Guessing a better match than Password Spraying (`T1110.003`), which would involve trying one or a small number of passwords across multiple accounts. | `queries.md` scoping/grouping search; `case-evidence-splunk-4625-short-scope.png` |

## Disposition

- [x] **Benign — authorized security simulation**

The detection was a true positive for password-guessing behavior, but the incident itself was an expected, authorized lab exercise generated from `WEC01`. Searches found no successful logons (4624), no account lockouts (4740), and therefore no evidence of compromise or post-authentication activity. If the source activity had been unauthorized, the disposition would change to malicious even if every password attempt failed; a successful logon would additionally require investigation of post-login activity and impact.

## Containment and Response Recommendations

*(Grounded in the observed pattern and finalized disposition above.)*

### Immediate containment
In a production environment, this pattern would justify: temporarily restricting/monitoring the source host's network access pending owner verification, and a precautionary password reset for `testuser1` even though it was never compromised — cheap insurance against a password that might already be weak enough to eventually succeed.

### Eradication/remediation
Not applicable in this lab — `10.10.10.30` (`WEC01`) is the designated, expected simulation source, not a real compromised host. In production, this step would involve verifying whether the source host itself is compromised or running unauthorized tooling.

### Recovery and validation
Sweep for the same failed-logon burst pattern against other accounts/hosts beyond this case's tightly scoped account/source pair, to rule out this being one visible piece of a wider attempt.

### Escalation/communication
In production: notify the system owner of the targeted host and the network/security team responsible for the source segment. In this lab, this step is documented rather than actually executed, since the "incident" is a self-contained authorized exercise.

## Detection and Visibility Improvements

- **Detection logic/tuning:** the validated 5-minute fixed-bucket threshold (`count>=5` per account/source) works but has a documented boundary-splitting weakness — activity split across a bucket boundary can evade the threshold. Converting to a rolling-window equivalent (or approximating one with overlapping bucket windows) is a scoped follow-up, not a defect in the current logic.
- **Likely false positives:** legitimate users who mistype a recently changed password repeatedly, service accounts retrying with stale/expired credentials, or misconfigured mapped drives retrying cached credentials.
- **Missing telemetry (the real finding of this case):** the Security channel's WEF forwarding was silently broken before this session's repair. Any environment with the same per-channel WEF ACL gap has zero SIEM visibility into this exact attack pattern despite full local endpoint logging — a detection blind spot that has nothing to do with query quality.
- **Hardening opportunity:** the local lockout policy was `Never`, specifically so this simulation wouldn't self-terminate — but that's a real exposed setting. A production host in this state would let an attacker attempt unlimited guesses with no lockout ever kicking in. Recommend a real lockout threshold balanced against denial-of-service risk, and/or network-level throttling (e.g., limiting RDP source rate) so detection isn't the only control standing between a weak password and compromise.
- **Follow-up scope:** add a broader sweep across other accounts/hosts for the same source/pattern before calling the wider environment's scope fully closed; use CASE-006 to build out the attacker-vs-legitimate-user discernment reasoning as its own validated case.

## Evidence Index

Screenshots in `screenshots/` (redacted as needed); full evidence log with descriptions in `docs/current-status.md`'s Evidence Captured table:
- Initial failed logon spike (platform view)
- Pivot showing top source + top targeted user
- Successful-logon outcome check (`case-evidence-splunk-4624-outcome-zero-results.png` — confirmed absent)
- Account lockout outcome check (`case-evidence-splunk-4740-outcome-zero-results.png` — confirmed absent)
- Final supporting screenshot confirming the detection report (`case-evidence-splunk-detection-report-verified.png`)

## Lessons Learned

- The hard part of this case was not writing SPL — it was discovering and repairing a real WEF telemetry gap that would have made this exact attack invisible to the SIEM despite being fully logged locally. That's a more realistic and more valuable SOC skill than the detection query itself.
- Confirming the outcome (4624/4740) with a live search rather than assuming "no lockout" from the policy setting alone is what this project's Validation-First Rule is actually for in practice, not just as a written rule — the difference between "the policy says lockout can't happen" and "I searched and confirmed it didn't happen" is the difference between an assumption and evidence.
- Distinguishing a real attacker's eventual success from a legitimate user's own forgotten-password struggle is a genuinely hard, evidence-limited problem that Windows auth logs alone can't fully resolve — source/timing consistency, behavioral baseline, and post-logon activity all matter more than the logon event itself. This case didn't need to resolve that ambiguity (clean 0-for-30), but CASE-006 is scoped specifically to practice it.
- This project's own docs disagreed with each other about which structure a completed case file should follow (`AGENTS.md`'s Case File Standard vs. `docs/incident-report-template.md`, the one `docs/plan.md`'s Common Completion Gate actually names) — worth reconciling before CASE-002 hits the same gap.

## Files in this case
- `timeline.md` — ordered event sequence with timestamps
- `iocs.md` — artifacts collected (sanitized)
- `queries.md` — investigation pivots (Splunk/Elastic/Wazuh)
- `screenshots/` — redacted evidence
