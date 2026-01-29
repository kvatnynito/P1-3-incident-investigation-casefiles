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

### 2) Confirm Sysmon events are flowing
- Purpose: confirm Sysmon ingestion (process/network)
- Expected: Sysmon Event ID 1 and/or 3 appear

