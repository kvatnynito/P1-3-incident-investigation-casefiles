# Queries / Pivots — CASE-001 Brute Force / RDP
Status: In progress — core scoping and threshold SPL validated; outcome correlation and tuning remain

## Goal
Document the minimal set of queries used to:
1) detect the spike,
2) identify source + targeted account,
3) confirm outcome (lockout/success),
4) check for follow-on activity.

Add your exact index/sourcetype names later. Keep these queries sanitized.

---

## Splunk (SPL) — Validated Queries

### 1) Confirm Security 4625 ingestion

```spl
host="wec01" LogName=Security EventCode=4625
```

This query confirmed genuine failed-logon events reached Splunk through WEC01 after the source Security-channel ACL repair.

### 2) Separate failed-logon patterns

```spl
host=wec01 LogName=Security EventCode=4625
| stats count by Account_Name Logon_Type Source_Network_Address
| sort -count
```

This grouped local Type 2/loopback failures separately from the controlled Type 3 network failures. `Account_Name` can be multivalue in this sourcetype, so displayed row counts must not be summed as if every row represents unique events.

### 3) Isolate the controlled RDP/NLA event set

```spl
host=wec01 LogName=Security EventCode=4625 Logon_Type=3 Source_Network_Address=10.10.10.30
```

Validated result: 30 events associated with the controlled source. Prior grouped evidence identifies `testuser1` as the target account.

### 4) Threshold detection

```spl
host=wec01 LogName=Security EventCode=4625 Logon_Type=3
| eval account=mvindex(Account_Name,-1)
| bin _time span=5m
| stats count by _time account Source_Network_Address
| where count>=5
```

Validated result: three qualifying buckets for `testuser1` from `10.10.10.30`, with counts of 13, 8, and 5. The account and source are not hardcoded into the detection logic.

## Detection Limitations and Tuning Work Still Required

- `bin _time span=5m` uses fixed buckets, not a rolling five-minute window; activity split across a boundary can evade the threshold.
- WEF ingestion delay and duplicated forwarded events can affect timing and counts.
- `mvindex(Account_Name,-1)` matched the worked example but must be validated across more Windows event shapes before production use.
- Expected service accounts, scanners, help-desk activity, and known administrative sources may require allowlisting or separate thresholds.
- Splunk Free cannot schedule alerts. The query is saved as the enabled, Private report `CASE-001 - Network Logon Failure Threshold`; automated alert execution and delivery are not validated.

## Queries Still Required

- Check for successful logons after the failure window.
- Confirm lockout and follow-on activity.
- Build the final time-normalized timeline and disposition pivots.

### Original placeholder retained for history

```spl
# TBD: search for failed logons (4625) in time window
