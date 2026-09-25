# PostgreSQL 16 V1R3 CAT I review

Benchmark: **Crunchy Data Postgres 16 STIG V1R3**  
CAT I controls: **11**  
Review date: **2026-09-25**

This document records the high-severity boundary decisions made before first lab testing. A CAT I control is not allowed to disappear behind a false/empty default.

| V-ID | STIG ID | Role behavior | First-cycle validation |
|---|---|---|---|
| V-261858 | CD16-00-000200 | Audits HBA methods. Any method outside gss/sspi/ldap/cert requires explicit organization approval evidence before remediation proceeds. | Reconcile every HBA rule to enterprise authentication design and approved exceptions. |
| V-261859 | CD16-00-000300 | Requires authorization-policy evidence before remediation. Does not invent GRANT/REVOKE state. | Compare roles/object privileges to SSP/data-owner authorization. |
| V-261882 | CD16-00-002700 | Requires documented procedure/evidence controlling and tracking PostgreSQL installation-account use. | Validate OS access controls and operational procedure for the postgres/software account. |
| V-261891 | CD16-00-003800 | Enforces password_encryption=scram-sha-256 for future password changes; post-remediation audit hard-fails when existing password credentials are non-SCRAM. | Reset any legacy credentials through approved credential management and reassess. |
| V-261892 | CD16-00-003900 | Hard-fails if HBA contains password or md5. SCRAM password authentication additionally requires AO approval evidence. No bulk HBA rewrite. | Validate all application/admin/replication/backup paths after approved HBA correction. |
| V-261894 | CD16-00-004100 | Resolves actual TLS key/cert/CA/CRL paths, reports file and parent-directory ownership/mode, and requires PKI protection evidence when private-key material exists. Does not relocate keys. | Verify authorized key access and FIPS cryptographic boundary. |
| V-261896 | CD16-00-004400 | Pre-remediation hard gate: OS FIPS indicator must be enabled; OpenSSL must be FIPS compliant and, for OpenSSL 3.x, the FIPS provider must be active. No automatic host conversion/reboot. | Validate RHEL/platform FIPS state and OpenSSL provider evidence. |
| V-261901 | CD16-00-005200 | Requires AO/application-owner at-rest determination and protection evidence. Audits pgcrypto availability but does not treat extension installation as proof data is encrypted. | Validate actual database/filesystem/disk protection or documented permitted N/A outcome. |
| V-261928 | CD16-00-008300 | Requires explicit classified/unclassified declaration. Classified deployments require NSA-approved crypto evidence; TLS can only be enabled through the guarded TLS path. | For classified systems validate SSL plus NSA-approved network encryption devices. |
| V-261930 | CD16-00-008500 | Requires data-owner/AO at-rest integrity-protection determination and evidence. No generic encryption mechanism is invented. | Validate all organization-defined protected data and storage components. |
| V-283674 | CD16-00-009300 | Pre-remediation version gate against the current PostgreSQL 16 minor pinned for the test cycle. Current value is 16.15 as of 2026-09-25. Does not perform blind package upgrades. | Confirm package/vendor source, 16.15 or newer current minor as policy is updated, and release-specific post-upgrade actions. |

## Important distinctions

- Hard-gating a CAT I control is not the same as remediating it.
- Evidence values are references/decisions, not secrets and not fabricated compliance.
- V-261892 deliberately refuses automatic HBA replacement because that can lock out DBAs, applications, replication, monitoring, and backup.
- V-261896 deliberately refuses automatic FIPS conversion because enabling host FIPS changes the OS boot/crypto lifecycle and requires reboot/platform validation.
- V-261901 and V-261930 deliberately do not install pgcrypto as a blanket answer: the checks permit multiple protection layers and require proof that the data identified by the owner is actually protected.
- V-283674 is time-sensitive. The pinned current minor must be reviewed whenever PostgreSQL publishes a new 16.x minor release.

## Team-test exit criteria for CAT I

Before this branch can be described as assessment-validated, every applicable CAT I must have:

1. successful pre-remediation prerequisite evaluation;
2. documented site/application evidence where required;
3. functional database/application testing after any relevant change;
4. authoritative V1R3 assessment result;
5. reconciliation of any scanner/manual result that differs from expected behavior.
