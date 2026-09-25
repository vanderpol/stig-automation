# PostgreSQL 16 V1R3 first-pass status

## Current state

Benchmark: **Crunchy Data Postgres 16 STIG V1R3**

- Current rule count: **111**
- Matrix enumeration: **111/111**
- Unique executable V-ID ownership: **111/111**
- Deterministic remediation: **partial**
- Technical audit/evidence handling: **first pass present**
- Syntax/lab validation: **not yet complete**
- Idempotency validation: **not yet complete**
- Authoritative V1R3 assessment reconciliation: **not yet complete**
- Anti-STIG: **deferred**

## What “111/111 executable ownership” means

Every current V-ID appears in one or more executable task paths as remediation, guarded remediation, technical audit, site evidence, application evidence, or negative-test evidence.

It does **not** mean all 111 requirements can or should be automatically remediated.

## Deterministic first-pass capability

Current safe implementation includes:

- live discovery of PostgreSQL data/config/HBA paths;
- PostgreSQL 16 major-version gate;
- merge-preserving addition of pgAudit to `shared_preload_libraries`;
- pgAudit baseline classes;
- pgAudit catalog/detail settings;
- connection/disconnection logging;
- common audit identity/time/session prefix;
- audit log file-creation mode;
- SCRAM-SHA-256 for newly stored passwords;
- client-visible error-detail restriction;
- post-edit `pg_file_settings` error check;
- explicit restart-required reporting rather than an automatic database restart.

## Explicitly guarded/site-owned areas

No broad mutation is performed for:

- `pg_hba.conf`;
- organization role/object privileges;
- extension deletion;
- package upgrades/removal;
- PPSM port/listen addresses;
- PKI/CA/CRL/private keys;
- FIPS conversion;
- at-rest encryption;
- classified-network encryption;
- central logging infrastructure;
- audit-capacity/alert infrastructure;
- application source/schema behavior.

## Known remaining engineering work

Before team-test readiness:

1. complete literal V1R3 check/fix reconciliation for each implemented technical setting;
2. verify the role parses under the repository's supported Ansible version;
3. strengthen configuration validation around restart-only parameters;
4. decide whether any currently guarded controls can be safely automated with explicit site inputs;
5. verify pgAudit behavior before and after the required restart;
6. finish provenance/test-risk row detail for all 111 controls;
7. review OS/package-specific behavior without assuming a universal PostgreSQL layout.

The branch should not be merged as a validated role until representative lab testing and current V1R3 assessment reconciliation are complete.

## Latest literal-check reconciliation

This review corrected several potentially misleading behaviors before lab testing:

- V-261899 example timeout/keepalive numbers are no longer treated as organizational defaults;
- V-261921 log timezone is site-selectable rather than silently forced;
- V-261917/V-261967 can merge an approved syslog facility without discarding existing log destinations;
- V-261879 now enforces mode 0600 on the actual discovered postgresql.conf and uses the discovered database-owner primary group;
- reloadable settings are followed by effective-state reporting from pg_settings so include-file overrides are visible;
- shared_preload_libraries remains explicitly restart-pending and is not represented as active until post-restart validation.
