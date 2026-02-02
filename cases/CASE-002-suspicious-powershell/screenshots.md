# Screenshots — CASE-002 Suspicious PowerShell
Status: Draft (to be updated during implementation)

Upload **case-specific, redacted evidence** here. These screenshots should support the timeline and findings documented in this case folder.

## Evidence checklist
- [ ] Starting signal (how the PowerShell activity was identified)
- [ ] Process creation evidence (PowerShell start event)
- [ ] Command line view (sanitize tokens/URLs as needed)
- [ ] Parent process context (what launched PowerShell)
- [ ] Child processes spawned (if any)
- [ ] Network activity tied to PowerShell (if any)
- [ ] File activity tied to PowerShell (if any)
- [ ] Final supporting screenshot that confirms the conclusion

## Suggested filenames (optional)
- `01-starting-signal.png`
- `02-powershell-process-start.png`
- `03-command-line.png`
- `04-parent-process.png`
- `05-child-processes.png`
- `06-network-activity.png`
- `07-file-activity.png`
- `08-final-confirmation.png`

## Redaction checklist (always)
Do NOT publish:
- WAN/public IPs, domains/DDNS, VPN endpoints/keys
- passwords, API keys, tokens, secrets
- full command lines containing sensitive tokens or unique identifiers

OK to publish (generally):
- representative RFC1918 ranges
- sanitized hostnames/usernames
- cropped views showing process relationships and investigation pivots
