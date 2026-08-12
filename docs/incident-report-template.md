# Incident Report Template

Use this structure in the active case `README.md` when the investigation is executed. Replace every placeholder with evidence-backed content; do not present planned or hypothetical activity as observed.

## Executive Summary

In a short paragraph, state what happened, affected system/account, time window, business/security impact, disposition, and recommended action.

## Scenario and Ground Truth

- Approved activity generated:
- Source and destination:
- Account/user:
- Exact start/end time:
- Expected telemetry:

## Initial Signal

- Alert or search that started the investigation:
- Platform and data source:
- Detection status: manual hunt / draft rule / validated rule

## Scope

| Field | Finding | Evidence reference |
|---|---|---|
| Time range | TBD | TBD |
| Host(s) | TBD | TBD |
| User/account(s) | TBD | TBD |
| Source/destination | TBD | TBD |
| Process/file/domain | TBD | TBD |

## Searches and Correlation

Summarize the searches used, what each proved or disproved, and any telemetry gaps. Put full query text in `queries.md`.

## Timeline

Summarize the significant sequence and link to `timeline.md`.

## Findings

Separate observed facts from analyst inference. State what happened, what did not happen, and what remains unknown.

## MITRE ATT&CK Mapping

| Tactic | Technique / sub-technique | Why the evidence supports it | Evidence reference |
|---|---|---|---|
| TBD | TBD | TBD | TBD |

Do not map a technique merely because it was expected in the scenario. Cite the observed behavior that supports the mapping.

## Disposition

- [ ] Benign
- [ ] Suspicious
- [ ] Malicious
- [ ] Needs more data

Explain why the evidence supports this disposition and what evidence would change it.

## Containment and Response Recommendations

### Immediate containment

TBD — proportional to the observed evidence.

### Eradication/remediation

TBD

### Recovery and validation

TBD

### Escalation/communication

TBD

## Detection and Visibility Improvements

- Detection logic/tuning:
- Likely false positives:
- Missing telemetry:
- Hardening opportunity:

## Evidence Index

Link sanitized screenshots or excerpts from `screenshots.md`. Never include secrets, raw malware, real personal information, WAN details, or unnecessary lab identifiers.

## Lessons Learned

State what the investigation taught, what was difficult, and what should be done differently next time.

