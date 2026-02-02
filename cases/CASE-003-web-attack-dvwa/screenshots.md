# Screenshots — CASE-003 Web Attack (DVWA)
Status: Draft (to be updated during implementation)

Upload **case-specific, redacted evidence** here. These screenshots should support the timeline and findings documented in this case folder.

## Evidence checklist
- [ ] Starting signal (web requests/errors/payload pattern observed)
- [ ] Example suspicious request/payload (sanitize as needed)
- [ ] Pivot: source attribution (source host/IP sanitized)
- [ ] Pivot: time window defined (start/end)
- [ ] Target context (which endpoint/app/path was targeted)
- [ ] Outcome evidence (attempt vs success indicators)
- [ ] Correlation to host activity on the DVWA server (if applicable):
  - [ ] suspicious process execution
  - [ ] outbound network connections
  - [ ] file changes
- [ ] Final supporting screenshot that confirms the conclusion

## Suggested filenames (optional)
- `01-starting-signal.png`
- `02-suspicious-request-payload.png`
- `03-source-attribution.png`
- `04-time-window.png`
- `05-target-context.png`
- `06-outcome-evidence.png`
- `07-host-correlation.png`
- `08-final-confirmation.png`

## Redaction checklist (always)
Do NOT publish:
- WAN/public IPs, domains/DDNS, VPN endpoints/keys
- passwords, API keys, tokens, secrets
- full payloads containing sensitive unique identifiers (sanitize)

OK to publish (generally):
- representative RFC1918 ranges
- sanitized hostnames/usernames
- cropped screenshots showing request patterns, pivots, and correlation steps
