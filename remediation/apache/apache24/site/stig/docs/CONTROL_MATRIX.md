# Apache Server 2.4 UNIX Site STIG V2R7 control matrix

Benchmark: V2R7, released 2026-05-23. 16 findings: 15 CAT II and 1 CAT III.

This ledger intentionally distinguishes Apache-remediable settings from application, PKI, architecture, PPSM, and process responsibilities.

Known current controls requiring explicit user/site responsibility include:
- V-214286 — RFC 5280-compliant certification-path validation when PKI is used.
- V-214287 — private-key access restricted to authenticated system administrators/designated PKI Sponsor.
- V-214300 — client certificates must chain to DoD PKI or DoD-approved PKI CAs.
- V-214304 — ports/services must comply with well-known/approved PPSM usage.

The automation may validate configuration facts around these requirements, but it must not download trust anchors, designate approved CAs/accounts, manufacture PPSM approval, or claim that an evidence flag establishes compliance.

The remaining V2R7 controls will be added here rule-by-rule from the current benchmark before being promoted to automated remediation.
