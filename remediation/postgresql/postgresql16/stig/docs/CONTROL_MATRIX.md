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
