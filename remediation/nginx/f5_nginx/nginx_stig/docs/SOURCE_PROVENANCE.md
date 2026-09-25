# F5 NGINX V1R1 source provenance

Development date: 2026-09-25.

Primary authority for every control is the current F5 NGINX STIG V1R1 benchmark (32 controls, V-278380 through V-278411). Implementation was derived from the current check/fix intent and repository lessons learned.

A public reference was reviewed for freshness before implementation: MITRE `ansible-nginx-stigready-hardening`, commit `91c566df3de481997cb510acb7a68ad2be88e78f` (2025-12-15). Its README states that it targets **Web Server SRG V2R3**, not F5 NGINX V1R1. Its substantive implementation predates the current product-specific benchmark; it is therefore **reference-only and not used as implementation authority or copied code**. GitHub reports its license as NOASSERTION; the repository contains `LICENSE.md`, so no material was incorporated pending license/current-benchmark reconciliation.

## Per-control ledger

All 32 controls are initially `ORIGINAL` or `COMMON` because no external implementation was materially used. Validation status is `UNTESTED` until representative lab execution and authoritative assessment.

| V-ID(s) | Provenance | Implementation type | Test risk | Reason |
|---|---|---|---|---|
| V-278381, V-278382, V-278386, V-278392, V-278394, V-278395, V-278397, V-278399, V-278408 | COMMON | REMEDIATION | MEDIUM | direct directive/account/file-permission mapping |
| V-278380, V-278383, V-278385, V-278387-V-278391, V-278393, V-278396, V-278398, V-278400-V-278406, V-278409-V-278411 | ORIGINAL | REMEDIATION/AUDIT/EVIDENCE as matrixed | HIGH | current product-specific logic, site inputs, architecture, PKI, auth, or effective-config parsing |
| V-278407 | ORIGINAL | EXTERNAL+VAR/EVIDENCE | HIGH | platform FIPS state cannot be created or proven by NGINX config alone |

## Validation status

- Current V-ID enumeration: complete (32/32).
- Executable/evidence representation: first pass complete (32/32).
- Syntax test: pending.
- Lab test: pending.
- Idempotency: pending.
- Authoritative assessment: pending.
- Anti-STIG: intentionally deferred until positive-baseline verification.
