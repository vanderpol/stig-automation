# Apache 2.4 UNIX STIG — First-Pass Status

## Benchmarks

- Server V3R3 (2026-05-28): 45 current findings.
- Site V2R7 (2026-05-23): 16 current findings.
- Historical benchmark controls are intentionally excluded.

## First-pass definition

Every current V-ID is represented in a control matrix and has an implementation disposition: deterministic remediation, site-supplied variable/audit, application responsibility, or evidence responsibility.

This is **implementation-complete for first testing**, not compliance-certified. Lab execution, syntax/idempotency testing, functional application testing, and authoritative assessment remain required.

## Server V3R3

All 45 current V-IDs are represented. Deterministic controls are remediated where the current check/fix permits a safe server-wide setting. Ambiguous administrative, application, architecture, operational, patch, and evidence controls remain explicit inputs/audits.

## Site V2R7

All 16 current V-IDs are represented. Site-specific PKI, application, PPSM, administrative authorization, network-zone, recovery, and evidence decisions remain end-user responsibilities. The role does not download or approve trust anchors/certificates or invent authorization boundaries.

## Duplicate review

Current candidate retained in both benchmarks:
- Server V-214244 ↔ Site V-214282: unused/vulnerable script mappings.

Both remain independently traceable unless DISA changes the current benchmarks.

## Test gate

Before calling either role release-ready:
1. Run Ansible syntax validation.
2. Deploy Server role to representative RHEL and Ubuntu test systems.
3. Re-run for idempotency.
4. Run Apache configtest and application functional tests.
5. Run authoritative Server V3R3 assessment.
6. Deploy Site role with a real site profile.
7. Validate PKI/application behavior where applicable.
8. Run authoritative Site V2R7 assessment.
9. Reconcile every mismatch by V-ID.
10. Only after a known-good compliant baseline, implement anti-STIG cases.

## Important design boundary

A successful Ansible run is not proof of STIG compliance. The readiness summary reports READY, SITE INPUT REQUIRED, or EVIDENCE REQUIRED, but the authoritative assessment and required organizational evidence determine compliance.
