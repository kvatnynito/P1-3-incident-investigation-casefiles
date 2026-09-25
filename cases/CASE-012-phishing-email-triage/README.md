# CASE-012: Phishing Email Header and Triage Investigation

**Status:** Active next (approved 2026-09-24, target ~2026-10-12) — no VM required
**Curriculum position:** Additional P1-3 case (outside the ten-lab Windows telemetry sequence, like CASE-003)

## Objective

Triage a suspicious email end to end: trace its delivery path from the `Received` headers, validate its SPF, DKIM, and DMARC results, analyze embedded links and attachment indicators without opening or detonating them, and write a supported disposition and remediation recommendation.

## Why This Case Exists

First-pass phishing triage is a headline duty in entry-level SOC postings (e.g., *"Perform first-pass phishing/email-threat triage (headers, links, attachments) and coordinate takedown/remediation with the team"* and *"Monitor DMARC/SPF/DKIM posture ... and flag anomalies for follow-up"*). Domain 8 had no evidence before this case.

## Prerequisites

- Fedora workstation only: `dig`, `sha256sum`, a text editor, and optionally `dkimpy` (`dkimverify`) for independent DKIM signature checking
- Two `.eml` samples, recorded as ground truth before analysis:
  1. **Known-good baseline** — a legitimate message from a major sender in Kevin's own mailbox (expected SPF/DKIM/DMARC pass)
  2. **Suspicious sample** — a real phishing message from a spam folder or a public phishing corpus
- Raw `.eml` files, full unredacted headers, and any attachments stay in the private `soc-detection-practice` companion. Only sanitized, defanged findings are published here.

## Ordered Steps

1. Record ground truth for each sample: source, how obtained, date, and why it was selected.
2. Export the full raw source (`.eml`) of both samples; never open attachments or click links.
3. Walk the `Received` chain bottom-to-top to reconstruct the delivery path (originating host/IP → relays → receiving MX) and note time deltas between hops.
4. Compare the visible `From`, `Return-Path` (envelope sender), `Reply-To`, and `Message-ID` domains for mismatches.
5. Read the receiving server's `Authentication-Results` for SPF, DKIM, and DMARC; state which domain each result is aligned to.
6. Independently check the sender domains' published posture with `dig` (SPF TXT, `_dmarc` TXT, DKIM selector from the `DKIM-Signature` `s=`/`d=` tags) and, where possible, verify the DKIM signature with `dkimverify`.
7. Extract and defang every URL; compare display text against the real target; check reputation using existing lookups only (urlscan.io search, VirusTotal URL/domain lookup) — do not submit Kevin's own links or personal data publicly.
8. For any attachment: record filename, MIME type, size, and SHA-256 from the saved file; check the hash reputation only. Never open, upload, or detonate it on the Fedora host.
9. Contrast the suspicious sample against the known-good baseline — which specific fields separate them.
10. Map to MITRE ATT&CK (e.g., T1566.001 Spearphishing Attachment / T1566.002 Spearphishing Link) based on what the sample actually contains.
11. Classify: benign, suspicious, malicious, or needs more data — with the evidence that supports it.
12. **Script (Kevin writes it himself):** a Python header parser using the stdlib `email` module (`email.message_from_file`, `msg.get_all('Received')`) that prints the hop chain and the SPF/DKIM/DMARC results for any `.eml`. Commit it with the case. Record what was self-written vs. given.
13. Write containment/remediation recommendations as an analyst would hand off: sender/domain block, mailbox search-and-purge, URL/domain block at the web gateway, and user/credential follow-up if clicked.

## Completion Evidence

- Delivery-path reconstruction with hop timing
- SPF/DKIM/DMARC results with alignment explained, cross-checked against live DNS
- Defanged URL and attachment-hash indicator table with reputation results
- Baseline-vs-suspicious comparison, ATT&CK mapping, disposition, and remediation recommendation
- Completed incident report using `../../docs/incident-report-template.md`

## Safety and Sanitization

- Never click links or open attachments from the suspicious sample. Treat the `.eml` as untrusted text.
- Defang all published indicators (`hxxps://example[.]com`).
- Redact Kevin's recipient address and any personal data from headers before publishing. No raw `.eml` files in this public repo.
