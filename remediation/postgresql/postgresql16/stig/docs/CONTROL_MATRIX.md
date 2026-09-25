# PostgreSQL 16 V1R3 control matrix

Benchmark: **Crunchy Data Postgres 16 STIG V1R3**  
Expected controls: **111**  
Status: **enumeration/classification in progress**

This ledger is deliberately created before remediation code. No control may silently disappear. A control is not considered covered until the V-ID, STIG ID, implementation type, provenance, risk, executable handling, and validation state are recorded here.

## Classification vocabulary

Implementation: `REMEDIATION | REMEDIATION/AUDIT | AUDIT | EVIDENCE | APP/EVIDENCE | N/A-SITE`

Provenance: `ORIGINAL | COMMON | ADAPTED | INHERITED | NEW-CURRENT`

Risk: `HIGH | MEDIUM | BASELINE`

## Initial reconciled controls

| V-ID | STIG ID | Sev | Initial handling | Provenance | Risk | Notes |
|---|---|---:|---|---|---|---|
| V-261857 | CD16-00-000100 | II | REMEDIATION/AUDIT | ORIGINAL | HIGH | Organization-defined max connections; never invent limits. |
| V-261858 | CD16-00-000200 | I | AUDIT/EVIDENCE | ORIGINAL | HIGH | Enterprise auth architecture/site approval required. |
| V-261859 | CD16-00-000300 | I | AUDIT/EVIDENCE | ORIGINAL | HIGH | Authorization must reconcile to SSP/site documentation. |
| V-261860 | CD16-00-000400 | II | REMEDIATION/AUDIT | ORIGINAL | HIGH | pgaudit/log identity plus application individual-user propagation. |
| V-261861 | CD16-00-000500 | II | REMEDIATION/AUDIT | ORIGINAL | HIGH | DoD minimum events plus organization-defined events. |
| V-261862 | CD16-00-000600 | II | REMEDIATION/AUDIT | ORIGINAL | HIGH | Ownership/superuser state must reconcile to designated personnel. |
| V-261863 | CD16-00-000700 | II | REMEDIATION | ORIGINAL | HIGH | pgaudit catalog/read behavior. |
| V-261864 | CD16-00-000800 | II | REMEDIATION/AUDIT | ORIGINAL | HIGH | Denials require logging and negative verification. |
| V-261865 | CD16-00-000900 | II | REMEDIATION/AUDIT | ORIGINAL | HIGH | Startup/session auditing. |
| V-261866 | CD16-00-001000 | II | REMEDIATION/AUDIT | ORIGINAL | HIGH | Event type/detail; shared logging capability. |
| V-261867 | CD16-00-001100 | II | REMEDIATION | COMMON | MEDIUM | Timestamp via log_line_prefix. |
| V-261868 | CD16-00-001200 | II | REMEDIATION | ORIGINAL | HIGH | Literal check requires %m %u %d %s; shared prefix uses a superset. |
| V-261869 | CD16-00-001300 | II | REMEDIATION/AUDIT | ORIGINAL | HIGH | Source/origin; hostname and remote endpoint semantics. |
| V-261870 | CD16-00-001400 | II | REMEDIATION/AUDIT | ORIGINAL | HIGH | Success/failure plus pgAudit detail settings. |
| V-261871 | CD16-00-001500 | II | REMEDIATION | COMMON | MEDIUM | User/process identity in shared prefix. |
| V-261872 | CD16-00-001600 | II | REMEDIATION/EVIDENCE | ORIGINAL | HIGH | Organization-defined extra audit detail; shared-account identity may be application-owned. |
| V-261873 | CD16-00-001700 | II | EVIDENCE | ORIGINAL | HIGH | Audit-failure shutdown decision is application-owner/AO dependent. |
| V-261874 | CD16-00-001800 | II | AUDIT/EVIDENCE | ORIGINAL | HIGH | FIFO/storage failure behavior spans PostgreSQL/OS/log platform. |
| V-261875 | CD16-00-002000 | II | REMEDIATION/AUDIT | COMMON | MEDIUM | log_file_mode 0600; syslog ownership differs. |
| V-261876 | CD16-00-002100 | II | REMEDIATION/AUDIT | COMMON | MEDIUM | Protect audit data from modification. |
| V-261877 | CD16-00-002200 | II | REMEDIATION/AUDIT | COMMON | MEDIUM | Protect audit data from deletion. |
| V-261878 | CD16-00-002300 | II | AUDIT/REMEDIATION | ORIGINAL | HIGH | PGDATA/PGLOG/pgAudit installation ownership plus approved superusers. |
| V-261879 | CD16-00-002400 | II | REMEDIATION/AUDIT | COMMON | MEDIUM | postgresql.conf and log protection. |
| V-261880 | CD16-00-002500 | II | AUDIT/REMEDIATION | ORIGINAL | HIGH | Product binary/library ownership is packaging/path dependent. |
| V-261881 | CD16-00-002600 | II | AUDIT/REMEDIATION | ORIGINAL | HIGH | Config/library/executable modification protection. |
| V-261882 | CD16-00-002700 | I | EVIDENCE | ORIGINAL | HIGH | Installation-account access/procedures; no invented authorized-user list. |
| V-261883 | CD16-00-002800 | II | AUDIT/EVIDENCE | ORIGINAL | HIGH | Dedicated software directory; relocation/reinstall is disruptive. |
| V-261884 | CD16-00-002900 | II | AUDIT/EVIDENCE | ORIGINAL | HIGH | Object ownership must reconcile to approved principals. |
| V-261885 | CD16-00-003000 | II | AUDIT/EVIDENCE | ORIGINAL | HIGH | Structure/logic modification privileges require approved-state comparison. |
| V-261886 | CD16-00-003200 | II | AUDIT/REMEDIATION | ORIGINAL | HIGH | Unapproved extensions; never DROP EXTENSION without explicit approval. |
| V-261887 | CD16-00-003300 | II | AUDIT/EVIDENCE | ORIGINAL | HIGH | Installed PostgreSQL packages must reconcile to required component list. |
| V-261888 | CD16-00-003400 | II | AUDIT/EVIDENCE | ORIGINAL | HIGH | External executable access depends on approved superusers/extensions. |
| V-261889 | CD16-00-003500 | II | REMEDIATION/AUDIT | ORIGINAL | HIGH | PPSM listen addresses/port are organization-defined and restart-sensitive. |
| V-261890 | CD16-00-003600 | II | AUDIT/EVIDENCE | ORIGINAL | HIGH | Unique identity must reconcile to organizational user/account design. |
| V-261891 | CD16-00-003800 | I | REMEDIATION/AUDIT | COMMON | HIGH | Enforce password_encryption=scram-sha-256; existing hashes require credential reset, not invention. |
| V-261892 | CD16-00-003900 | I | GUARDED REMEDIATION/AUDIT | ORIGINAL | HIGH | password/md5 HBA methods fail; bulk auth change can cause lockout. |
| V-261893 | CD16-00-004000 | II | REMEDIATION/EVIDENCE | ORIGINAL | HIGH | PKI CRL and cert validation require site trust material. |
| V-261894 | CD16-00-004100 | I | REMEDIATION/EVIDENCE | ORIGINAL | HIGH | Private-key paths/permissions and approved access are site-owned. |
| V-261895 | CD16-00-004200 | II | AUDIT/EVIDENCE | ORIGINAL | HIGH | Certificate CN/user-map semantics depend on identity architecture. |
| V-261896 | CD16-00-004400 | I | AUDIT/EVIDENCE | ORIGINAL | HIGH | Host/platform FIPS boundary; no silent host conversion. |
| V-261897 | CD16-00-004500 | II | AUDIT/EVIDENCE | ORIGINAL | HIGH | Nonorganizational identities require organizational documentation. |
| V-261898 | CD16-00-004600 | II | AUDIT/EVIDENCE | ORIGINAL | HIGH | Admin/user separation; do not revoke privileges without approved state. |
| V-261899 | CD16-00-004700 | II | REMEDIATION/AUDIT | ORIGINAL | HIGH | Timeout/keepalive values are organization-defined; zero fails current check. |
| V-261900 | CD16-00-004900 | II | REMEDIATION/EVIDENCE | ORIGINAL | HIGH | ssl=on plus valid site certificate/key; enabling blindly may break startup. |
| V-261901 | CD16-00-005200 | I | AUDIT/EVIDENCE | ORIGINAL | HIGH | At-rest protection depends on AO/data-owner decision and actual protected data. |
| V-261902 | CD16-00-005300 | II | AUDIT/EVIDENCE | ORIGINAL | HIGH | Security-function schema isolation is application/database-design owned. |
| V-261903 | CD16-00-005400 | II | EVIDENCE | ORIGINAL | HIGH | Organization data-transfer policy and operational procedures. |
| V-261904 | CD16-00-005600 | II | AUDIT/REMEDIATION | ORIGINAL | HIGH | PGDATA/log/backup access; recursive mutation needs platform-aware review. |
| V-261905 | CD16-00-005700 | II | APP/EVIDENCE | ORIGINAL | HIGH | Input validation/prepared statements require schema/application review. |
| V-261906 | CD16-00-005800 | II | APP/EVIDENCE | ORIGINAL | HIGH | Dynamic execution requires source-code/application review. |
| V-261907 | CD16-00-005900 | II | APP/EVIDENCE | ORIGINAL | HIGH | Dynamic execution input defenses require code review. |
| V-261908 | CD16-00-006000 | II | REMEDIATION/APP-EVIDENCE | ORIGINAL | HIGH | client_min_messages=error plus application error-message review. |
| V-261909 | CD16-00-006100 | II | REMEDIATION/AUDIT | COMMON | MEDIUM | Restrict client error detail; protect server logs separately. |
| V-261910 | CD16-00-006200 | II | REMEDIATION/EVIDENCE | ORIGINAL | HIGH | Automatic termination triggers are organization-defined; may be N/A. |
| V-261911 | CD16-00-006400 | II | APP/EVIDENCE | ORIGINAL | HIGH | Security labels in storage are conditional and schema/application-specific. |
| V-261912 | CD16-00-006500 | II | APP/EVIDENCE | ORIGINAL | HIGH | Security labels in process are conditional and schema/application-specific. |
| V-261913 | CD16-00-006600 | II | APP/EVIDENCE | ORIGINAL | HIGH | Security labels in transmission are conditional and architecture-specific. |
| V-261914 | CD16-00-006700 | II | AUDIT/EVIDENCE | ORIGINAL | HIGH | DAC must reconcile to data-owner policy; no generic GRANT/REVOKE baseline. |
| V-261915 | CD16-00-006800 | II | AUDIT/EVIDENCE | ORIGINAL | HIGH | Privileged functions/extensions must reconcile to approved roles and AO risk acceptance. |
| V-261916 | CD16-00-006900 | II | APP/EVIDENCE | ORIGINAL | HIGH | SECURITY DEFINER/elevated module execution requires documented application need. |
| V-261917 | CD16-00-007000 | II | GUARDED REMEDIATION/EVIDENCE | ORIGINAL | HIGH | Central syslog is required; facility/destination architecture is site-owned. |
| V-261918 | CD16-00-007200 | II | EVIDENCE | ORIGINAL | HIGH | Audit storage capacity is organization-defined and infrastructure-owned. |
| V-261919 | CD16-00-007300 | II | EVIDENCE | ORIGINAL | HIGH | 75% storage alert requires site monitoring/notification integration. |
| V-261920 | CD16-00-007400 | II | EVIDENCE | ORIGINAL | HIGH | Real-time audit failure alert requires site monitoring/notification integration. |
| V-261921 | CD16-00-007500 | II | REMEDIATION/AUDIT | COMMON | MEDIUM | log_timezone must map to UTC; site timezone policy retained explicitly. |
| V-261922 | CD16-00-007600 | II | REMEDIATION | COMMON | MEDIUM | Shared log prefix includes %m millisecond timestamp. |
| V-261923 | CD16-00-007700 | II | AUDIT/EVIDENCE | ORIGINAL | HIGH | Logic-module installation privileges require approved users; dev-only N/A possible. |
| V-261924 | CD16-00-007800 | II | AUDIT/EVIDENCE | ORIGINAL | HIGH | Configuration/database change privileges require approved-state comparison. |
| V-261925 | CD16-00-007900 | II | REMEDIATION/AUDIT | ORIGINAL | HIGH | Denied configuration changes must be logged; negative verification required. |
| V-261926 | CD16-00-008000 | II | GUARDED REMEDIATION/AUDIT | ORIGINAL | HIGH | PPSM-approved port is site-owned and changing it is restart/connectivity sensitive. |
| V-261927 | CD16-00-008100 | II | APP/EVIDENCE | ORIGINAL | HIGH | Reauthentication on role/privilege changes spans application/session design. |
| V-261928 | CD16-00-008300 | I | EVIDENCE | ORIGINAL | HIGH | Classified-only NSA-approved network cryptography; N/A in unclassified environment. |
| V-261929 | CD16-00-008400 | II | REMEDIATION/EVIDENCE | ORIGINAL | HIGH | DOD-approved CA trust is site PKI material; do not invent trust anchors. |
| V-261930 | CD16-00-008500 | I | REMEDIATION/EVIDENCE | NEW-CURRENT | HIGH | V1R3 severity changed to CAT I; at-rest integrity is site/data-owner dependent. |
| V-261931 | CD16-00-008600 | II | REMEDIATION/EVIDENCE | ORIGINAL | HIGH | At-rest confidentiality; may be DB, filesystem, or disk control. |
| V-261932 | CD16-00-008800 | II | REMEDIATION/EVIDENCE | ORIGINAL | HIGH | Conditional on data-owner requirement; SSL alone may not prove full path. |
| V-261933 | CD16-00-008900 | II | REMEDIATION/EVIDENCE | ORIGINAL | HIGH | Reception protection; validate transport boundary. |
| V-261959 | CD16-00-011500 | II | REMEDIATION/AUDIT | ORIGINAL | HIGH | Privileged activity audit; include denial behavior. |
| V-261960 | CD16-00-011600 | II | REMEDIATION | COMMON | MEDIUM | Connection/disconnection timestamps and identity. |
| V-261961 | CD16-00-011700 | II | REMEDIATION/AUDIT | ORIGINAL | HIGH | Must reconstruct concurrent sessions/workstations. |
| V-261962 | CD16-00-011800 | II | REMEDIATION/AUDIT | ORIGINAL | HIGH | pgaudit read/write/ddl/role semantics require literal-check validation. |
| V-261963 | CD16-00-011900 | II | REMEDIATION/AUDIT | ORIGINAL | HIGH | Negative object-access verification. |
| V-261964 | CD16-00-012000 | II | REMEDIATION/AUDIT | ORIGINAL | HIGH | Direct DB access audit. |
| V-261965 | CD16-00-012200 | II | AUDIT/EVIDENCE | ORIGINAL | HIGH | System FIPS state; role must not casually convert host into FIPS mode. |
| V-261966 | CD16-00-012300 | II | AUDIT/EVIDENCE | ORIGINAL | HIGH | FIPS + data-owner cryptographic requirement. |
| V-261967 | CD16-00-012400 | II | REMEDIATION/AUDIT | ORIGINAL | HIGH | Central logging facility is organization-defined. |
| V-283674 | CD16-00-009300 | I | AUDIT/EVIDENCE | NEW-CURRENT | HIGH | Vendor-supported/current PostgreSQL 16 package level; no blind upgrade. |

## Gate

The table above is **not yet the complete 111-control enumeration**. No remediation tasks are being represented as complete until the exact V1R3 package ledger is fully populated. This explicit gate prevents the documentation/executable drift encountered in earlier lockdown work.
