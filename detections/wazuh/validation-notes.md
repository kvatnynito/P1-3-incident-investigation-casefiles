# Wazuh Validation Notes
Status: Draft (to be updated during implementation)

This file is my **“is Wazuh working?” checklist**.

Wazuh is used for monitoring + alerts. Before I rely on it for a case, I validate:
- the manager/dashboard is reachable
- agents (if used) are connected
- events are arriving
- alerts show up when I trigger test activity
- timestamps make sense

---

## Quick setup info (fill in later)
- Wazuh server/manager name: TBD
- Dashboard URL/location (not public): TBD
- Agents used? (yes/no): TBD
- Windows endpoints monitored: TBD
- Linux endpoints monitored: TBD

---

## How to use this file (later)
1) Open the Wazuh Dashboard
2) Confirm the manager is healthy
3) Confirm agents/events are visible
4) Trigger a small test action (safe) and confirm it appears
5) Capture 1–2 redacted screenshots for evidence

---

## 1) Platform health check
**Goal:** confirm Wazuh is running and accessible

- [ ] I can log into the Wazuh Dashboard
- [ ] Wazuh manager service is running (if I’m checking locally)
- [ ] No obvious error banners or “disconnected” warnings

**Notes:** TBD

---

## 2) Agent connectivity (if using agents)
**Goal:** confirm monitored machines are connected

- [ ] At least 1 Windows agent shows as connected
- [ ] (Optional) At least 1 Linux agent shows as connected
- [ ] Agents are reporting recently (last check-in time is recent)

**Notes (agent names):**
- Windows agent(s): TBD
- Linux agent(s): TBD

---

## 3) Event visibility (are logs arriving?)
**Goal:** confirm Wazuh is receiving events (not empty)

- [ ] I can view recent events for a monitored endpoint
- [ ] I can filter by a specific host/agent and still see events
- [ ] Events appear within the last 15 minutes

**Notes (what I see):** TBD

---

## 4) Test alert: failed logon (Windows)
**Goal:** confirm Wazuh can surface authentication-related activity

**Test I will run (later):**
- Trigger 2–3 failed logons on a Windows endpoint (safe test)

**Expected:**
- I see an event and/or alert tied to failed authentication activity
- It includes host/user context (even if the field names differ)

- [ ] Test performed
- [ ] Evidence observed in Wazuh
- [ ] Screenshot captured (redacted)

**Notes:** TBD

---

## 5) Test alert: Sysmon / process activity (if Sysmon is collected)
**Goal:** confirm process visibility (useful for PowerShell case)

**Test I will run (later):**
- Run a simple command on a Windows endpoint (ex: open PowerShell and run `whoami`)

**Expected:**
- A process-related event shows up (or an alert, depending on rules)
- Command/process context is visible (even if limited)

- [ ] Test performed
- [ ] Evidence observed in Wazuh
- [ ] Screenshot captured (redacted)

**Notes:** TBD

---

## 6) Timestamp sanity check
**Goal:** confirm the timeline makes sense

- [ ] Events appear close to the time I generated them
- [ ] No major time drift (hours/days off)
- [ ] Timezone used for this case: TBD

**Notes:** TBD

---

## Evidence to capture later (screenshots)
Upload redacted screenshots to:
- `screenshots/` (global) OR
- the case `screenshots/` folder (if it’s case-specific)

Checklist:
- [ ] Dashboard showing recent activity
- [ ] Agent status view (if agents are used)
- [ ] One example event (redacted)
- [ ] One example alert (redacted)

---

## Troubleshooting notes (fill in later)
If something is missing, I will check:
- agent status (connected/disconnected)
- time range filters
- whether the endpoint is generating activity
- whether log collection is enabled for that source

**What I fixed / learned:** TBD
