# Splunk Validation Searches
Status: Draft (to be updated during implementation)

These searches are used to quickly confirm:
- data is arriving (WEF/Sysmon/Security logs)
- key fields are present
- timestamps look correct

## Before I can write working searches
To fill in the SPL below, I will first confirm:
- [ ] Which index the Windows logs land in (TBD)
- [ ] Which sourcetype is used for Security logs (TBD)
- [ ] Which sourcetype is used for Sysmon logs (TBD)
- [ ] Which field names are available (EventCode vs event.code, user vs Account_Name, src_ip vs IpAddress, etc.)

Once data is flowing, I will:
1) Run a broad search for the last 15 minutes  
2) Identify index/sourcetype/fields from the event sidebar  
3) Update the searches below with the real values  

---

# Planned validation searches

## 1) Confirm Windows Security events are flowing
- Purpose: confirm Security log ingestion (logons/failures)
- Expected: events returned within the last 15 minutes


## 2) Confirm Sysmon events are flowing
- Purpose: confirm Sysmon ingestion (process/network)
- Expected: Sysmon Event ID 1 and/or 3 appear

## 3) Confirm failed logons are visible (4625)
- Purpose: validate authentication telemetry for brute force cases
- Expected: Security Event ID 4625 events appear

## 4) Quick field sanity check
- Purpose: confirm key fields exist and are consistently extracted
- Expected: you can list/see fields like host, user, src_ip, EventCode
