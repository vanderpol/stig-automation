# Tomcat 9 V3R4 provenance/current-check review

## Result

Retrospective review was performed against the current Apache Tomcat Application Server 9 STIG V3R4 (79 findings) and the repository implementation derived from the project-owner-supplied v0.3 baseline.

The review found a material coverage problem: the existing matrix claimed classification coverage for all 79 findings, while executable remediation/audit reconciliation found 14 current controls that were missing or only partially represented.

## Current gaps found

- V-222926 — manager simultaneous-session limit
- V-222962 — LDAP realm authentication for management applications
- V-222965 — secure LDAP/LDAPS
- V-222968 — FIPS-validated secured connectors
- V-222970 — manager application network restriction
- V-222971 — proxy/load-balancer mutual authentication
- V-222974 — trusted cluster network
- V-222976 — customized manager error pages
- V-222979 — 10-minute manager idle timeout
- V-222980 — LockOutRealm use
- V-222981 — LockOutRealm failureCount=5
- V-222982 — LockOutRealm lockOutTime=600
- V-223006 — ISSO approval of management-role users
- V-223009 — connector address completeness (partial implementation existed)

Audit visibility has been added for all 14 so they can no longer disappear from test output. They are **not** considered remediated merely because audit messages now exist.

## Source/provenance conclusion

The repository README establishes the project-owner-supplied `tomcat9_stig_ansible_rhel8_rhel9_v0.3` project as the implementation baseline. Existing task logic is therefore inherited from that internal baseline, with later local adaptations.

Ansible-Lockdown TOMCAT-9-STIG exists as a maintained public remediation project and was consulted as comparison material during this retrospective review. No evidence available in this repository establishes that the supplied v0.3 baseline was copied from Ansible-Lockdown, so public-repository inheritance is not asserted.

Apache Tomcat's community review of the DISA STIG is useful technical commentary and highlights that some STIG recommendations have semantic/operability concerns. It is treated as review material, not compliance authority.

## Current-release discipline

V3R4 is the implementation authority. V-222927, V-222929, and V-222936 were removed before the current release and must not be reintroduced merely because historical automation contains them.

## Test consequence

Tomcat should **not yet be described as having all 79 current controls implemented**. The 14 gaps above must be resolved as remediation, audit/evidence, or explicit N/A/site-owned behavior and then validated on RHEL 8/9 before the same tester-handoff status used for Apache is appropriate.

Detailed per-control status is in `remediation/tomcat/tomcat9/stig/docs/SOURCE_PROVENANCE.md`.
