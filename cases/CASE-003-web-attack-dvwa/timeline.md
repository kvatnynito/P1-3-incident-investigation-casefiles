# Timeline — CASE-003 Web Attack (DVWA)
Status: Draft (to be updated during implementation)

## Time Normalization
- Timezone used in this case: TBD
- Notes: confirm timestamps align across web/app logs and host telemetry

## Timeline (Fill in during investigation)

| Time (TBD) | Host | Log Source | Event Type | Summary | Notes / Pivot |
|---|---|---|---|---|---|
| TBD | TBD | Web/App logs | Request spike / payload | Suspicious requests begin | Identify pattern + source |
| TBD | TBD | Web/App logs | Error/response change | Possible success indicator | Note response codes |
| TBD | TBD | Sysmon (optional) | 1 / 3 / 11 | Host activity observed (if any) | Process/network/file correlation |
| TBD | TBD | TBD | TBD | End of activity window | Document stop condition |

## Notes (What to capture)
- Request indicators (paths, parameters, payload patterns)
- Source host/IP (sanitized)
- Correlated host events (if attack leads to execution)
