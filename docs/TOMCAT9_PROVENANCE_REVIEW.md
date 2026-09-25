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

This round closed the deterministic portions that can be safely automated and converted the remaining architecture/process requirements into explicit guarded inputs/evidence. The 14 controls no longer silently disappear from execution, but mixed controls still require site evidence and lab validation.

## Source/provenance conclusion

The repository README establishes the project-owner-supplied `tomcat9_stig_ansible_rhel8_rhel9_v0.3` project as the implementation baseline. Existing task logic is therefore inherited from that internal baseline, with later local adaptations.

Ansible-Lockdown TOMCAT-9-STIG exists as a public remediation project and current Ansible-Lockdown documentation labels it maintained/remediation-capable. Rechecked 2026-09-25, the role README still does not state a DISA Tomcat benchmark version and lists RHEL 7/8, CentOS 7/8, and Ubuntu 16.04/18.04/20.04. The repository view exposes no tagged release and did not provide enough commit-date evidence to establish that the implementation was refreshed after V3R4 was released on 2026-02-25. It is therefore comparison/reference material only, not a V3R4 authority. No evidence in this repository establishes that the supplied v0.3 baseline was copied from Ansible-Lockdown, so public-repository inheritance is not asserted.

Apache Tomcat's community review of the DISA STIG is useful technical commentary and highlights that some STIG recommendations have semantic/operability concerns. It is treated as review material, not compliance authority.

## Current-release discipline

V3R4 is the implementation authority. V-222927, V-222929, and V-222936 were removed before the current release and must not be reintroduced merely because historical automation contains them.

## Test consequence

All 79 current V3R4 controls are now represented as remediation, guarded remediation, audit/evidence, or explicit N/A/site-owned behavior. The newly added manager LDAP/LDAPS, LockOutRealm, session, network restriction, connector-address, FIPS, proxy mutual-authentication, cluster-evidence, manager-error-page, and ISSO-approval logic remains **untested**. Tomcat is therefore implementation-complete for this review round but is not yet assessment-verified or ready to be called compliant.

Detailed per-control status is in `remediation/tomcat/tomcat9/stig/docs/SOURCE_PROVENANCE.md`.


## Current V3R4 wording/assessment anomalies

The review found several places where literal benchmark wording deserves tester attention:

- **V-222971:** current check/fix wording mixes legacy `clientAuth` terminology with an `SSLHostConfig` attribute name/value that does not match current Tomcat 9 product syntax. Tomcat 9 documents `certificateVerification="required"` for `SSLHostConfig`. The role uses the product-valid `certificateVerification="required"` form and `CLIENT-CERT` application authentication rather than writing an invalid `certificationVerification="true"` attribute. Treat any scanner/manual-assessor discrepancy here as a benchmark/tool reconciliation issue and capture the exact evidence.
- **V-222979:** the current check references `webapps/manager/META-INF/web.xml`, while normal servlet deployment uses `WEB-INF/web.xml`; the same check also explicitly accepts the 10-minute value in `$CATALINA_BASE/conf/web.xml`. The role therefore sets the global `conf/web.xml` timeout to 10 minutes so the current assessment path is unambiguous. Hosted applications may override their own timeout when authorized.
- **V-222976:** the description mentions 401/403/404 pages, while the current check/fix text names 401/402/403. The role follows the current check/fix files (401/402/403) and does not overwrite 404 unnecessarily.

These are not reasons to ignore the benchmark. They are reasons to preserve exact assessment output and distinguish a product-valid configuration from a potentially inconsistent literal check.
