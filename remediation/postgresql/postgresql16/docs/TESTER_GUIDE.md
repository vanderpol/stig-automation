# PostgreSQL 16 V1R3 Tester Guide

## Purpose

This guide is for the first hands-on validation of the Ansible remediation role for the **Crunchy Data Postgres 16 STIG V1R3**.

This is an initial validation build. A successful Ansible run is **not** proof of STIG compliance. The goal of this test cycle is to verify:

- safe discovery of the real PostgreSQL installation;
- correct Ansible behavior;
- service and application functionality;
- idempotency;
- correct handling of CAT I prerequisites;
- current V1R3 assessment results;
- any differences between the STIG check text, PostgreSQL behavior, and the automation.

Do not begin on a production database.

## Before you start

Record the following in `remediation/postgresql/postgresql16/docs/TEST_REPORT.md`:

- tester name and date;
- exact Git commit or branch;
- operating system and version;
- PostgreSQL server version and package source;
- pgAudit version and package source;
- Ansible version;
- current STIG/assessment content version;
- database topology: standalone, replica, cluster, or HA framework;
- backup/restore method available for the test system.

Take an approved backup or snapshot before applying remediation.

## 1. Prepare the repository

Check out the PostgreSQL development branch:

    git checkout main
    git pull

Copy the example inventory:

    cp inventories/lab/hosts.postgresql16.example.yml inventories/lab/hosts.yml
    cp inventories/lab/group_vars/postgresql16.yml.example inventories/lab/group_vars/postgresql16.yml

Edit the copied files for the real test system.

Do not commit:

- passwords;
- password hashes;
- private keys;
- tokens;
- production connection strings;
- sensitive database data.

Use Ansible Vault or the site's approved secret-management mechanism where secrets are unavoidable.

## 2. Review CAT I prerequisites first

Read:

    remediation/postgresql/postgresql16/stig/docs/CAT_I_REVIEW.md

Several CAT I controls intentionally stop the role before remediation when required site evidence or platform prerequisites are missing.

Important examples include:

- authentication-method approvals;
- authorization-policy evidence;
- installation-account control/tracking evidence;
- AO approval for password authentication;
- host FIPS/OpenSSL readiness;
- PKI/private-key protection evidence;
- at-rest protection determination;
- classified/unclassified applicability;
- current PostgreSQL 16 minor release.

This behavior is intentional. Do not bypass a CAT I prerequisite merely to get the playbook to finish.

## 3. Verify Ansible connectivity

Run:

    ansible postgresql16 -m ping

Resolve connectivity, privilege-escalation, or Python issues before continuing.

## 4. Run preflight

Run:

    ansible-playbook playbooks/postgresql16_preflight.yml

Preflight is intended to gather state without changing the database.

Review the output for:

- detected PostgreSQL version;
- detected data directory;
- detected `postgresql.conf`;
- detected `pg_hba.conf`;
- PostgreSQL owner/group;
- HBA authentication methods;
- role and superuser state;
- connection limits;
- pgAudit availability;
- TLS certificate/key/CA/CRL paths;
- TLS file and parent-directory permissions;
- FIPS indicator and OpenSSL provider state;
- server port and listen addresses;
- logging and syslog configuration;
- installed extensions;
- current PostgreSQL minor release;
- required site/application evidence.

If discovery identifies the wrong instance, wrong cluster, wrong configuration file, or wrong HBA file, stop testing and report it.

## 5. Run check mode and review the diff

Run:

    ansible-playbook playbooks/postgresql16_stig.yml --check --diff

Review every proposed file change.

Pay particular attention to:

- `shared_preload_libraries` — existing libraries must be preserved;
- `postgresql.conf` permissions;
- pgAudit parameters;
- logging changes;
- SCRAM password-storage setting;
- session/keepalive settings if site values were supplied;
- syslog settings if a facility was supplied;
- TLS enablement if explicitly requested;
- cluster-wide connection limits.

Do not proceed if the diff would remove an existing library, overwrite an unrelated site setting, or make an unexplained architecture change.

## 6. Apply remediation

Run:

    ansible-playbook playbooks/postgresql16_stig.yml

Save the complete non-secret output with the test record.

The role may stop because a CAT I prerequisite is unmet. Treat that as a useful test result, not an automation failure.

## 7. Handle restart-required settings

The role intentionally does **not** restart PostgreSQL automatically.

If `shared_preload_libraries`, `max_connections`, or another restart-sensitive setting changed, follow the site's approved restart/change procedure.

Before restart, record the reported pending-restart state.

After restart, confirm:

    sudo -u postgres psql -AtX -c "SHOW shared_preload_libraries;"
    sudo -u postgres psql -AtX -c "SELECT name, pending_restart FROM pg_settings WHERE pending_restart ORDER BY name;"

Confirm that:

- `pgaudit` is present when required;
- no unexpected restart-pending settings remain;
- PostgreSQL starts without configuration errors.

## 8. Validate PostgreSQL and pgAudit

Check PostgreSQL service and logs using the platform's normal service-management process.

Confirm that pgAudit is available and functional.

Generate representative test activity in a disposable test database and verify that audit records contain the required identity, timestamp, session, object, and event details.

For findings requiring denied/failed-operation evidence, perform the negative tests only against a disposable test database.

Do not intentionally break authorization on a production or shared database.

## 9. Functional application testing

Test the normal operational paths that the database supports.

At minimum, where applicable, validate:

- application login and transactions;
- DBA/admin login;
- monitoring account access;
- backup account access;
- replication;
- HA/failover management;
- TLS clients;
- connection pooling;
- scheduled jobs;
- audit-log ingestion/offload;
- certificate authentication;
- enterprise authentication.

Authentication and `pg_hba.conf` behavior deserve extra scrutiny because an apparently compliant change can still lock out applications or administrators.

## 10. Run idempotency test

Run the remediation playbook a second time:

    ansible-playbook playbooks/postgresql16_stig.yml

A stable system should show no unexplained changes on the second run.

Record every unexpected second-run change as an idempotency defect.

## 11. Run the authoritative V1R3 assessment

Use the current **Crunchy Data Postgres 16 STIG V1R3** assessment content.

Record:

- Pass;
- Fail;
- Not Applicable;
- Not Reviewed;
- every unexpected V-ID.

Do not classify the role as compliant merely because Ansible completed successfully.

For every unexpected assessment result, compare:

1. the literal current V1R3 check text;
2. the actual PostgreSQL effective state;
3. the Ansible task for that V-ID;
4. any required site/application evidence;
5. whether an include file or runtime/restart state changes the effective setting.

## 12. CAT I controls requiring deliberate review

The current CAT I set is documented in:

    remediation/postgresql/postgresql16/stig/docs/CAT_I_REVIEW.md

Give special attention to:

- V-261858 — enterprise authentication / approved exceptions;
- V-261859 — authorization policy;
- V-261882 — installation-account control;
- V-261891 — SCRAM password storage and existing legacy hashes;
- V-261892 — HBA password/md5 methods and AO approval;
- V-261894 — private-key protection;
- V-261896 — FIPS/OpenSSL;
- V-261901 — at-rest confidentiality;
- V-261928 — classified-system transport protection;
- V-261930 — at-rest integrity;
- V-283674 — current supported PostgreSQL 16 minor.

Do not waive or bypass these controls locally just to produce a green test run.

## 13. What to include in a useful defect report

For each problem, include:

- Git commit SHA;
- V-ID;
- OS/version;
- PostgreSQL version/package source;
- pgAudit version/package source;
- relevant non-secret configuration;
- exact Ansible task/failure/change;
- whether check mode differed from apply mode;
- PostgreSQL service/config validation result;
- application impact;
- idempotency result;
- authoritative V1R3 assessment result;
- proposed interpretation or concern.

Do not include credentials, private keys, password hashes, tokens, or production data.

## 14. Where to store results

Place sanitized team test artifacts under:

    remediation/postgresql/postgresql16/tests/results/

Use:

    docs/POSTGRESQL16_TEST_REPORT.md

as the test-report template.

## 15. What counts as a successful first lab cycle

A useful first validation cycle should produce:

- successful discovery of the correct PostgreSQL instance;
- reviewed check-mode diff;
- controlled remediation apply;
- approved restart where required;
- clean PostgreSQL startup/config validation;
- functional application/database testing;
- second-run idempotency results;
- authoritative V1R3 assessment results;
- reconciliation notes for every unexpected V-ID.

A test cycle that uncovers defects is still successful if the evidence is complete enough to correct the role.
