# Splunk Validation Searches
Status: Draft (to be updated during implementation)

These searches are used to quickly confirm:
- data is arriving (WEF/Sysmon/Security logs)
- key fields are present
- timestamps look correct

## What to add later
- Index + sourcetype names used in this lab (sanitized)
- 3–5 “quick checks” that always work

## Planned validation searches
### 1) Confirm Windows Security events are flowing
- Purpose: confirm Security log ingestion (e.g., logons/failures)
- Expected: events returned within last X minutes

```spl
# TBD: search Security events in last 15m

