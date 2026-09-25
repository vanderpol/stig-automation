# PostgreSQL 16 benchmark authority

## Selected benchmark

- Product: Crunchy Data Postgres 16
- Authority: DISA / DoD Cyber Exchange
- STIG: Crunchy Data Postgres 16 STIG
- Version / Release: **V1R3**
- Release date: **2026-07-01**
- DISA package: `U_CD_Postgres_16_V1R3_STIG.zip`
- Expected current rule count: **111**
- Severity summary: **11 CAT I / High, 100 CAT II / Medium, 0 CAT III / Low**
- Scope: PostgreSQL 16 only
- Legacy Crunchy Data PostgreSQL STIG: explicitly out of scope; DISA sunset that benchmark in the July 2026 release.

## Authority rule

The current DISA V1R3 benchmark is the implementation authority. Third-party mirrors, scanner audit files, public Ansible roles, older STIG releases, and vendor examples may be used for cross-checking but must not override current DISA check/fix semantics.

The July 2026 DISA release announcement is the authoritative release confirmation. The exact V-ID/control ledger must be reconciled to the V1R3 DISA package before remediation implementation is declared first-pass complete.

## V1R3 delta noted during intake

The V1R3 release changes V-261930 (CD16-00-008500) from CAT II/Medium to CAT I/High. This control therefore receives HIGH test scrutiny.

## Development gate

Do not implement controls ahead of benchmark enumeration/classification merely because an equivalent setting appears obvious. This role follows:

`benchmark -> enumerate -> classify -> provenance -> implement -> literal-check reconciliation -> product semantics -> test`
