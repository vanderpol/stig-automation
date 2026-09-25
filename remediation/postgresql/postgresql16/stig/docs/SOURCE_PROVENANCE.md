# PostgreSQL 16 source provenance

## Benchmark source

| Source | Use | Authority |
|---|---|---|
| DISA / DoD Cyber Exchange, Crunchy Data Postgres 16 STIG V1R3, released 2026-07-01 | Requirement/check/fix authority | PRIMARY |
| DISA package `U_CD_Postgres_16_V1R3_STIG.zip` | Exact benchmark/supporting appendices | PRIMARY |
| PostgreSQL 16 upstream documentation | Product syntax and semantics | SECONDARY |
| PostgreSQL upstream versioning/release policy | V-283674 current supported/current-minor cross-check | SECONDARY |
| pgAudit upstream documentation | Audit extension syntax/behavior | SECONDARY |
| RHEL/platform vendor documentation | Packaging, FIPS, service, filesystem behavior | SECONDARY |
| Cyber Trackr V1R3 mirror of the DISA XCCDF | Control enumeration and literal check/fix cross-check while developing | TERTIARY |
| Third-party scanner audit content | Discovery/cross-check only | TERTIARY |

## Provenance policy

Implementation provenance is recorded per V-ID in `CONTROL_MATRIX.md` and must follow repository `docs/PROVENANCE_POLICY.md`.

No public Ansible/PostgreSQL lockdown implementation has been adopted as implementation authority during this intake round. If one is consulted later, record exact repository, tag/commit, file/control location, license, benchmark freshness, material used, and local changes before its logic is incorporated.

## Current-release freshness

DISA's July 2026 quarterly announcement lists Crunchy Data Postgres 16 STIG V1R3 and simultaneously sunsets the older Crunchy Data PostgreSQL STIG. The PostgreSQL 16 role therefore does not inherit legacy CD12 assumptions merely because older automation exists.

## Enumeration checkpoint — 2026-09-25

The development matrix was reconciled to the V1R3 rule sequence and programmatically counted at **111 unique V-IDs**. The apparent numeric gap at V-261937 is legitimate: CD16-00-009300 is V-283674, followed by V-261938 / CD16-00-009400. This checkpoint records enumeration only; it is not an assessment or implementation-completeness claim.

## Current-version checkpoint — 2026-09-25

PostgreSQL upstream identifies **16.15** as the current PostgreSQL 16 minor release and PostgreSQL 16 as supported through 2028-11-09. The role pins 16.15 as the V-283674 test-cycle prerequisite rather than performing an uncontrolled package upgrade. This value is intentionally time-sensitive and must be reviewed when a new PostgreSQL 16 minor is released.
