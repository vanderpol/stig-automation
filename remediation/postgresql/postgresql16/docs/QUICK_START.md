# PostgreSQL 16 V1R3 tester quick start

## Scope

This branch targets only the current **Crunchy Data Postgres 16 STIG V1R3**.

It is an **initial validation build**, not a compliance-certified release. The role has complete 111-control executable ownership, but many controls correctly remain audit/evidence/application-owned rather than deterministic remediation.

Do not use the role first on a production database.

## Before testing

Record:

- exact Git commit/branch;
- operating system and version;
- PostgreSQL 16 exact server/package version and package source;
- pgAudit package/version/source;
- Ansible version;
- database service/cluster topology;
- current authoritative assessment content/version;
- whether the target is standalone, replicated, clustered, or managed by another HA framework.

Take an approved backup/snapshot and confirm the database can be restored.

## Inventory

From the repository root:

    cp inventories/lab/hosts.postgresql16.example.yml inventories/lab/hosts.yml
    cp inventories/lab/group_vars/postgresql16.yml.example inventories/lab/group_vars/postgresql16.yml

Edit the copies for the real lab target and provide only approved organization/site values.

Never commit passwords, private keys, tokens, connection strings containing secrets, or certificate private material.

## Validation sequence

1. Verify connectivity:

       ansible postgresql16 -m ping

2. Run discovery and read-only preflight:

       ansible-playbook playbooks/postgresql16_preflight.yml

   Review:
   - discovered data/config/HBA paths;
   - PostgreSQL major/version;
   - pgAudit availability;
   - role/superuser/connection-limit state;
   - HBA authentication methods;
   - SSL/PKI settings;
   - port/listen settings;
   - log destination/time zone;
   - filesystem modes/ownership;
   - host FIPS state;
   - site/application evidence requirements.

3. Preview changes:

       ansible-playbook playbooks/postgresql16_stig.yml --check --diff

4. Review the diff carefully. In particular, confirm the role does not replace unrelated values in `shared_preload_libraries`.

5. Apply remediation:

       ansible-playbook playbooks/postgresql16_stig.yml

6. If `shared_preload_libraries` changed, the role reports a required PostgreSQL restart but intentionally does not perform it. Follow the site's approved database restart/change process.

7. Confirm PostgreSQL starts cleanly and review logs for configuration, pgAudit, TLS, authentication, extension, and application errors.

8. Functionally test:
   - normal application authentication;
   - administrator authentication;
   - replication/HA if applicable;
   - backup/monitoring accounts;
   - TLS clients;
   - application transactions;
   - audit ingestion/offload.

9. Run the playbook a second time. Record any unexpected changes as an idempotency defect.

10. Run the current authoritative **V1R3** assessment and reconcile every unexpected V-ID.

11. For findings whose checks require denied operations, perform those negative tests only on a disposable test database and retain the generated audit evidence.

## High-risk first-cycle areas

Give extra scrutiny to:

- `shared_preload_libraries` merging and pgAudit startup;
- HBA/authentication findings, especially V-261892;
- certificate/CRL/private-key and DOD-approved trust findings;
- V-261930, whose severity changed to CAT I in V1R3;
- FIPS findings and actual host crypto state;
- PPSM port/listen-address controls;
- role/object/extension ownership and authorization;
- audit storage, alerts, and central offload;
- package/support findings;
- application-owned SQL injection, dynamic execution, security-label, and reauthentication requirements.

## Important boundary

Ansible success is not proof of STIG compliance. This role intentionally leaves organization, application, PKI, FIPS, encryption, monitoring, and authorization decisions to approved evidence where automation cannot legitimately determine them.

Use `remediation/postgresql/postgresql16/docs/TEST_REPORT.md` for test results.
