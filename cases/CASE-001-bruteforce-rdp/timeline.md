# Timeline — CASE-001 Brute Force / RDP
Status: Draft (to be updated during implementation)

## Time Normalization
- Timezone used in this case: TBD
- Notes: confirm endpoint/collector/SIEM timestamps align

## Timeline (Fill in during investigation)
Use one row per important step. Keep it simple and consistent.

| Time (TBD) | Host | Event Source | Event ID / Type | Summary | Notes / Pivot |
|---|---|---|---|---|---|
| TBD | TBD | Windows Security | 4625 | Failed logon spike begins | Identify logon type + failure reason |
| TBD | TBD | Windows Security | 4625 | Continued failures | Pivot: top source IP / username |
| TBD | TBD | Windows Security | 4740 | Account lockout (if observed) | Confirm targeted account |
| TBD | TBD | Windows Security | 4624 | Successful logon (if observed) | Confirm logon type, source, user |
| TBD | TBD | Sysmon | 3 | Network connections around auth attempts (optional) | Correlate with source host |
| TBD | TBD | Windows Security | 4672 / 4688 | Privilege use / process activity (if observed) | Follow-on behavior check |
| TBD | TBD | TBD | TBD | End of activity window | Document stop condition |

## Notes (What to capture)
- Logon Type (e.g., 10 for RDP) if applicable
- Failure reason/substatus (helps distinguish mistyped passwords vs lockout policy)
- Source host/IP and whether it’s expected in lab
- Any follow-on suspicious activity after a successful logon
