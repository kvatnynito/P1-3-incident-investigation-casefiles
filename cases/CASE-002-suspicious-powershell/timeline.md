# Timeline — CASE-002 Suspicious PowerShell
Status: Draft (to be updated during implementation)

## Time Normalization
- Timezone used in this case: TBD
- Notes: confirm endpoint/collector/SIEM timestamps align

## Timeline (Fill in during investigation)

| Time (TBD) | Host | Event Source | Event ID / Type | Summary | Notes / Pivot |
|---|---|---|---|---|---|
| TBD | TBD | Sysmon | 1 | PowerShell process creation | Capture full command line + parent |
| TBD | TBD | Sysmon | 1 | Child process spawned (if any) | Identify children, persistence attempts |
| TBD | TBD | Sysmon | 3 | Network connection (if any) | Destination, port, purpose |
| TBD | TBD | Windows Security | 4688 (optional) | Process creation (if enabled) | Correlate with Sysmon |
| TBD | TBD | TBD | TBD | End of activity window | Document stop condition |

## Notes (What to capture)
- Full command line (sanitize tokens/URLs if needed)
- Parent process name and command line
- Any outbound network destinations (sanitize if needed)
- Any files created or downloaded (hashes if applicable)
