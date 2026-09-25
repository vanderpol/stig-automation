# PostgreSQL 16 source provenance

## Benchmark source

| Source | Use | Authority |
|---|---|---|
| DISA / DoD Cyber Exchange, Crunchy Data Postgres 16 STIG V1R3, released 2026-07-01 | Requirement/check/fix authority | PRIMARY |
| DISA package `U_CD_Postgres_16_V1R3_STIG.zip` | Exact benchmark/supporting appendices | PRIMARY |
| PostgreSQL 16 upstream documentation | Product syntax and semantics | SECONDARY |
| pgAudit upstream documentation | Audit extension syntax/behavior | SECONDARY |
| RHEL/platform vendor documentation | Packaging, FIPS, service, filesystem behavior | SECONDARY |
| Third-party STIG mirrors/scanner audit content | Discovery/cross-check only | TERTIARY |

## Provenance policy

Implementation provenance is recorded per V-ID in `CONTROL_MATRIX.md` and must follow repository `docs/PROVENANCE_POLICY.md`.

No public Ansible/PostgreSQL lockdown implementation has been adopted as implementation authority during this intake round. If one is consulted later, record exact repository, tag/commit, file/control location, license, benchmark freshness, material used, and local changes before its logic is incorporated.

## Current-release freshness

DISA's July 2026 quarterly announcement lists Crunchy Data Postgres 16 STIG V1R3 and simultaneously sunsets the older Crunchy Data PostgreSQL STIG. The PostgreSQL 16 role therefore does not inherit legacy CD12 assumptions merely because older automation exists.
