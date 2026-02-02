# Splunk (Searches)
Status: Draft (to be updated during implementation)

Splunk is where I **search and explore logs** to answer investigation questions like:
- “Who is failing logins the most?”
- “Where did the traffic come from?”
- “Did a successful login happen after failures?”

In Splunk, these are called **searches** and they use a language called **SPL**.

---

## What’s inside this folder

### `validation-searches.md`
These are my “sanity check” searches to confirm Splunk is receiving data.
I use these before doing any investigation so I don’t waste time chasing empty data.

Examples of what I validate:
- Are Windows Security logs showing up?
- Are Sysmon logs showing up?
- Do timestamps look correct?

### `case-searches.md`
These are my “investigation pivots” for specific cases (CASE-001, CASE-002, etc.).
They help me move step-by-step through an investigation:
failed logons → top user → source IP → success/lockout → follow-on activity

---

## How this connects to `/cases`
Each case has a `queries.md` file that documents what I ran.
That case file should reference the relevant searches in this folder.

Think:
- Case file = the story
- This folder = the Splunk tools used to find the facts

---

## Current status
Right now these are templates/placeholders.
When I implement the lab, I’ll paste working SPL searches here and keep them sanitized.
