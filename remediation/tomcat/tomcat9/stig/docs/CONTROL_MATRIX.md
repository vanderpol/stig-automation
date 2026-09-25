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


## V3R4 provenance/current-check reconciliation result

A September 2026 retrospective comparison against the current 79-control V3R4 benchmark initially found 14 controls that were missing or only partially represented by executable remediation/audit logic. This round closed those gaps as follows:

| V-ID | Requirement | Current treatment |
|---|---|---|
| V-222926 | Manager simultaneous sessions | REMEDIATION — SSP value required; maxActiveSessions applied when manager exists |
| V-222962 | Management applications LDAP realm | REMEDIATION — installed management apps require site-supplied JNDIRealm inputs |
| V-222965 | Secure LDAP authentication | REMEDIATION — LDAPS required for management JNDIRealm |
| V-222968 | FIPS-validated secured connectors | REMEDIATION/EVIDENCE — remediation hard-stops until RHEL/Java FIPS evidence is supplied, then configures FIPSMode=on |
| V-222970 | Restrict manager application access | REMEDIATION — manager context uses SSP-approved RemoteCIDRValve or RemoteAddrValve semantics |
| V-222971 | Mutual authentication with proxy/load balancer | REMEDIATION/EVIDENCE — explicit proxied connector/application scope required; certificateVerification=required plus CLIENT-CERT, or approved risk acceptance |
| V-222974 | Cluster trusted network | AUDIT/EVIDENCE — trusted/private network or coordinated EncryptInterceptor evidence required |
| V-222976 | Customize manager default error pages | REMEDIATION — current check/fix 401/402/403 manager JSPs replaced with generic responses |
| V-222979 | Manager idle timeout 10 minutes | REMEDIATION — global conf/web.xml timeout set to 10 when manager exists |
| V-222980 | LockOutRealm for management | REMEDIATION — Engine-level server.xml LockOutRealm after explicit application-impact acknowledgement |
| V-222981 | LockOutRealm failureCount=5 | REMEDIATION |
| V-222982 | LockOutRealm lockOutTime=600 | REMEDIATION |
| V-223006 | Management-role users approved by ISSO | EVIDENCE — explicit approval evidence required |
| V-223009 | Connector address attribute | REMEDIATION — every active connector must have an SSP-approved address mapping |

The original classification totals above came from the supplied v0.3 project matrix and should not be interpreted as proof of validated coverage. The current implementation status is tracked in SOURCE_PROVENANCE.md.
