# PostgreSQL 16 STIG — issues and concerns

This is a living engineering/test document. It records conditions that can create false compliance, outages, broad blast radius, or assessor discrepancies.

## 1. Organization-defined values are not defaults

Several controls require organization-defined session limits, approved roles, ports, authentication mechanisms, audit events, cryptographic protections, logging facilities, or other site decisions. The role must require supplied values/evidence rather than inventing them.

## 2. Authentication changes can lock out administrators/applications

`pg_hba.conf` changes are HIGH risk. Enterprise authentication, certificate authentication, GSS/LDAP, local maintenance access, replication, monitoring, backup, and application service accounts must be modeled explicitly. Never replace the whole file with a generic STIG template.

## 3. PKI is site-owned

Do not generate fake trust anchors, select an arbitrary CA, assume certificate mappings, or overwrite operational certificates. Certificate/key/CRL paths and trust decisions require explicit site inputs and evidence.

## 4. pgAudit is a cross-control dependency

Many audit controls converge on `shared_preload_libraries`, `pgaudit.log`, PostgreSQL logging, and log format. Manage these as a coherent capability while retaining per-V-ID traceability. Do not let one task overwrite another control's required audit classes.

## 5. shared_preload_libraries requires careful merging

Never replace an existing library list with only `pgaudit`. Preserve required existing libraries, validate PostgreSQL configuration, and distinguish reload-required settings from restart-required settings.

## 6. Restart versus reload

Some PostgreSQL parameters require restart. Remediation must identify disruptive actions, validate configuration first, and gate restarts rather than hiding them in handlers.

## 7. FIPS is a platform boundary

The STIG checks host FIPS state for cryptographic-module controls. Converting an existing host to FIPS mode is architecture-affecting and can be disruptive. Initial behavior should audit/hard-stop with evidence requirements rather than silently enabling host FIPS.

## 8. At-rest encryption is not solely a PostgreSQL setting

The benchmark permits/depends on database, filesystem, disk, and physical protections according to data-owner requirements. Installing `pgcrypto` does not by itself prove that protected data is encrypted. These controls require evidence-aware handling.

## 9. Central logging is site-owned

The STIG expects audit offload and checks syslog behavior. The destination/facility and enterprise log architecture must be supplied by the organization. Do not assume `LOCAL0` is approved simply because it appears in example fix text.

## 10. Object/role remediation can destroy application behavior

Do not automatically revoke database/object privileges, drop extensions, remove roles, alter ownership, or delete objects merely because observed state differs from a generic baseline. Compare to explicit approved-state inputs and default to audit/evidence for application-owned authorization.

## 11. Package upgrades are not blind remediation

V-283674 requires a supported/current product. Report installed/current package state and fail clearly when policy requires action; do not perform an uncontrolled major/minor package upgrade that can trigger database migration or outage.

## 12. Assessor-path fidelity

Use the exact current V1R3 check/fix semantics and paths. Equivalent hardening elsewhere is not proof that the current assessment will pass.

## 13. Platform scope remains to be proven

PostgreSQL 16 packaging, service names, PGDATA discovery, pgAudit packaging, log locations, and FIPS behavior vary by distribution/repository. Platform support will be explicit; unsupported combinations must fail preflight rather than guess.

## 14. No compliance claim from Ansible success

Successful playbook execution is only remediation evidence. Compliance requires current V1R3 assessment plus organization/application evidence.

## 15. Anti-STIG deferred

Negative/regression automation will not be built until a representative PostgreSQL 16 system reaches an authoritative known-good V1R3 baseline.


## 16. Effective PostgreSQL configuration can differ from edited files

PostgreSQL supports included configuration files and later definitions can override values written to the primary `postgresql.conf`. Therefore, a successful `lineinfile` change is not sufficient evidence that the runtime setting is effective.

The role now reloads reloadable settings and reports effective values from `pg_settings`. Restart-only settings such as `shared_preload_libraries` remain pending until an approved restart and post-restart verification.

## 17. Organization-defined examples are not policy defaults

V-261899 includes example timeout/keepalive values, but its fix text explicitly says to set them to organizational requirements. Those example numbers are not role defaults. The role requires explicit approved nonzero inputs before changing these parameters.

Similarly, V-261921 permits a UTC-mappable desired time zone. The role does not silently change operational log timezone unless a site value is supplied.

## 18. Central syslog requires both PostgreSQL and enterprise evidence

For V-261917 and V-261967, supplying an approved `postgres16_syslog_facility` enables guarded PostgreSQL configuration. Existing log destinations are preserved and `syslog` is merged in rather than replacing them. Compliance still requires evidence that the selected facility is routed/offloaded according to the organization's centralized logging design.

## 19. V-261879 requires actual config-file protection

The current check explicitly evaluates `postgresql.conf` ownership and mode. The role therefore protects the actual server-reported configuration file as the discovered database-owner account/group with mode `0600`; it does not assume `$PGDATA/postgresql.conf` is the effective path.


## 20. CAT I prerequisites deliberately block remediation

The role now executes technical CAT I prerequisites before configuration changes. A target can therefore stop before remediation for missing authorization/install-account evidence, unsupported authentication methods, missing AO approval for password authentication, non-FIPS host crypto state, missing at-rest determination, classified-system crypto gaps, or an out-of-date PostgreSQL minor release.

This is intentional. A successful remediation run must not imply CAT I coverage while a known CAT I prerequisite remains unmet.

## 21. V-283674 is time-sensitive

As of 2026-09-25, PostgreSQL upstream lists 16.15 as the current PostgreSQL 16 minor. The test-cycle default is pinned to 16.15 and must be deliberately updated when a newer PostgreSQL 16 minor is released. The role reports/fails version state but does not perform blind package upgrades.

## 22. Parsed file state versus runtime state

For shared_preload_libraries, the role now reads PostgreSQL's parsed file state via pg_file_settings and compares it with the running setting. This protects pending configuration from being overwritten and exposes restart-sensitive drift. pg_settings.pending_restart is also reported after remediation.
