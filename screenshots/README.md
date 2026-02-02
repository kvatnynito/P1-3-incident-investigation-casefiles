# Screenshots (Global)
Status: Draft (to be updated during implementation)

This folder is for **shared / cross-case** screenshots that apply to the overall lab and tooling.

## What belongs here
Use this folder for screenshots that are useful across multiple cases, such as:
- Platform landing pages / health checks (Splunk, Elastic, Wazuh)
- Proof that ingestion is working (high-level “events are arriving” views)
- Dashboards or Discover searches that are not tied to a single case
- Environment overview screenshots (sanitized)

## What does NOT belong here
Case-specific evidence should go inside:
`cases/CASE-XXX-<name>/screenshots/`

Examples of case-specific evidence:
- The initial alert/signal for a case
- Timeline pivots for that case
- IOC confirmations for that case
- Screenshots used directly in a case’s README/timeline/queries

## Redaction checklist (always)
Do NOT publish:
- WAN/public IPs, domains/DDNS, VPN endpoints/keys
