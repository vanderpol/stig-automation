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
- Static current-check/vendor reconciliation: complete (2026-09-25).
- Syntax test: pending.
- Lab test: pending.
- Idempotency: pending.
- Authoritative assessment: pending.
- Anti-STIG: intentionally deferred until positive-baseline verification.


## 2026-09-25 vendor-semantics reconciliation

Current NGINX documentation was used as a semantic cross-check, not as an alternative compliance authority. Material conclusions:

- `ssl_ocsp_responder` supports HTTP responder URLs; the V1R1 fix text shows an HTTPS responder in one place.
- `ssl_stapling_file` is a file containing a pre-generated OCSP response; it is not documented as a writable response cache. The V1R1 instruction to create an empty cache file is therefore not implemented.
- `ssl_ciphers` uses the OpenSSL cipher-list syntax; TLS 1.3 cipher-suite control is distinct and may require OpenSSL/provider configuration (for example via `ssl_conf_command` where appropriate). The role therefore does not claim that its TLS <=1.2 cipher string proves V-278405/V-278407.
- NGINX documents TLS 1.2/TLS 1.3 as the current `ssl_protocols` default, but V-278381 explicitly requires the directive to be present, so the role sets it explicitly.

These discrepancies are retained as HIGH-risk assessment items and should be reported upstream to the benchmark maintainer if lab validation confirms the conflict.
