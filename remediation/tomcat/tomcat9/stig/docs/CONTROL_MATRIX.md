# Apache Tomcat 9 DISA STIG V3R4 — control/remediation matrix

Baseline: **Apache Tomcat Application Server 9 STIG V3R4 (79 findings)**.

Classification: `AUTO` = deterministic remediation; `AUTO-VAR` = deterministic once an SSP/ISSO/site value is supplied; `EXTERNAL+VAR` = Tomcat/RHEL configuration can be automated but external platform/process evidence remains; `HUMAN/EVIDENCE`/`HUMAN/ARCH`/`PROCESS` = a human or lifecycle decision cannot safely be invented by Ansible.

This repository copy is sourced from the previously developed project matrix. See the role defaults and tasks for implementation boundaries.

## Classification totals

- AUTO: 45
- AUTO-VAR: 25
- EXTERNAL+VAR: 2
- HUMAN/EVIDENCE: 5
- HUMAN/ARCH: 1
- PROCESS: 1

## Stabilization rule

No control is promoted to AUTO merely because a plausible hardening setting exists. Site authorization, RMF applicability, PKI provenance, approved networks/connectors, and production patch approval remain explicit inputs/evidence.


## V3R4 provenance/current-check reconciliation finding

A September 2026 retrospective comparison against the current 79-control V3R4 benchmark found that the existing summary totals overstated implemented coverage. The following current controls are not yet fully represented by executable remediation/audit logic. They remain part of the benchmark and must not be reported as implemented until closed.

| V-ID | Requirement | Intended type | Status | Finding |
|---|---|---|---|---|
| V-222926 | Manager simultaneous sessions | AUTO-VAR | GAP | Variable exists but no task currently applies/checks manager maxActiveSessions. |
| V-222962 | Management applications LDAP realm | AUTO-VAR | GAP | LDAP variables exist but no current task configures/verifies JNDIRealm. |
| V-222965 | Secure LDAP authentication | AUTO-VAR | GAP | No task currently verifies LDAPS connectionURL. |
| V-222968 | FIPS-validated secured connectors | EXTERNAL+VAR | GAP | No task currently validates FIPSMode plus OS/Java FIPS evidence. |
| V-222970 | Restrict manager application access | AUTO-VAR | GAP | Management CIDR regex exists but is not applied to manager context.xml. |
| V-222971 | Mutual authentication with proxy/load balancer | EXTERNAL+VAR | GAP | Proxy mTLS variable exists but current XML logic does not implement current SSLHostConfig/client-cert semantics. |
| V-222974 | Cluster trusted network | HUMAN/ARCH | GAP | Cluster/trusted-network variables exist but are not audited. |
| V-222976 | Customize manager default error pages | AUTO/AUDIT | GAP | No task currently checks/customizes manager JSP error pages. |
| V-222979 | Manager idle timeout 10 minutes | AUTO | GAP | No task currently enforces manager session timeout. |
| V-222980 | LockOutRealm for management | AUTO-VAR | GAP | No task currently creates/verifies LockOutRealm. |
| V-222981 | LockOutRealm failureCount=5 | AUTO | GAP | No task currently enforces failureCount. |
| V-222982 | LockOutRealm lockOutTime=600 | AUTO | GAP | No task currently enforces lockOutTime. |
| V-223006 | Management-role users approved by ISSO | AUDIT | GAP | No task currently enumerates management-role users against an approved list. |
| V-223009 | Connector address attribute | AUTO-VAR | PARTIAL | XML sets address only for ports supplied in connector-address map; it does not verify every connector has an SSP-approved address. |

The original classification totals above describe the previously developed project matrix, not verified executable coverage. Use this reconciliation section and SOURCE_PROVENANCE.md for current implementation status until the gaps are closed.
