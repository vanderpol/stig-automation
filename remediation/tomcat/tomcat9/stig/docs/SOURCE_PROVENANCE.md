# Apache Tomcat 9 V3R4 - Retrospective Source Provenance

**Status:** retrospective reconstruction. The Tomcat role predates the repository provenance policy.

**Current authority:** Apache Tomcat Application Server 9 STIG V3R4, 79 findings. Current-check comparison was performed against V3R4 reference material. Historical releases are not implementation authority.

## Source lineage established

1. The repository README explicitly identifies the project-owner-supplied `tomcat9_stig_ansible_rhel8_rhel9_v0.3` project as the implementation baseline. Existing v0.3-derived tasks are therefore classified **INHERITED (internal project baseline)** where no later substantial redesign is known.
2. Subsequent repository reconciliation changed several inherited tasks (service-account UID handling, audit package installation, truststore password handling, XML namespace handling, booleans, path discovery, and tester UX). Those changes are local adaptations on top of the inherited baseline.
3. Ansible-Lockdown publishes a public TOMCAT-9-STIG remediation project under the MIT license. Current Ansible-Lockdown documentation labels it maintained/remediation-capable, but the role README does not identify a DISA Tomcat benchmark version and still describes RHEL 7/8, CentOS 7/8, and Ubuntu 16.04/18.04/20.04 assumptions. The current DISA V3R4 benchmark was released 2026-02-25. This review could not establish that the public role is V3R4-aligned or that its implementation was refreshed after that release, so it is reference material only. No public-repository inheritance is asserted.
4. Apache Tomcat community review material was consulted as technical commentary because it identifies semantic/operability concerns in the DISA Tomcat STIG; it is not implementation authority.

## Source inventory

| Source | Role in this repository | Version/date | License/authority |
|---|---|---|---|
| DISA Apache Tomcat Application Server 9 STIG | Primary compliance authority for every current V-ID | V3R4, released 2026-02-25 | U.S. Government / DISA authority |
| Project-owner supplied `tomcat9_stig_ansible_rhel8_rhel9_v0.3` | Direct implementation baseline for pre-policy Tomcat work | v0.3, supplied to this project | Internal project baseline; upstream ancestry unresolved |
| Ansible-Lockdown TOMCAT-9-STIG | Retrospective implementation comparison only | Public `devel`; benchmark alignment unverified | MIT |
| Apache Tomcat 9 configuration documentation | Product-semantic reference for Realm, Manager, Connector, SSLHostConfig, etc. | Current Tomcat 9 docs consulted during review | Apache Software Foundation |
| Apache Tomcat community DISA STIG review | Secondary technical commentary/errata signal | Review based on 2021 STIG, last updated 2022 | Apache community commentary; not compliance authority |

## Reference locations

- Current DISA benchmark authority: https://public.cyber.mil/stigs/downloads/
- Current V3R4 check/fix comparison view used during this retrospective review: https://www.stigviewer.com/stigs/apache_tomcat_application_server_9/v/V3R4
- Public Ansible-Lockdown comparison role: https://github.com/ansible-lockdown/TOMCAT-9-STIG
- Apache Tomcat 9 product documentation: https://tomcat.apache.org/tomcat-9.0-doc/
- Apache Tomcat community review of the DISA STIG: https://cwiki.apache.org/confluence/spaces/TOMCAT/pages/199536782/Community+Review+of+DISA+STIG
- Direct implementation baseline: project-owner-supplied `tomcat9_stig_ansible_rhel8_rhel9_v0.3` archive; not a public source.

The public Ansible-Lockdown role was rechecked on 2026-09-25. Its project documentation currently labels TOMCAT-9-STIG maintained/remediation-capable, but the role README does not identify V3R4, lists RHEL 7/8, CentOS 7/8 and Ubuntu 16.04/18.04/20.04 as its supported platforms, and the repository page exposes no tagged release. The fetched GitHub view did not provide a latest-commit date sufficient to prove that the implementation was refreshed after V3R4's 2026-02-25 release. It therefore remains a secondary comparison source, not implementation authority.

## Important finding

The initial reconciliation found **14 current V3R4 controls with missing or partial implementation/audit coverage**. This round closed the deterministic gaps where safe and converted the remaining architecture/process items into explicit evidence/guardrail controls. The review therefore found and corrected substantive coverage issues, not just attribution issues.

### Shared per-control metadata

The following fields apply to every row below unless a row's source basis says otherwise:

- **Benchmark / primary authority:** Apache Tomcat Application Server 9 STIG V3R4, released 2026-02-25.
- **Retrospective contributor/date:** stig-automation provenance reconciliation, September 2026.
- **Internal baseline location:** project-owner-supplied `tomcat9_stig_ansible_rhel8_rhel9_v0.3` archive.
- **Public comparison source/version/location/license:** Ansible-Lockdown TOMCAT-9-STIG, public `devel` view rechecked 2026-09-25, https://github.com/ansible-lockdown/TOMCAT-9-STIG, MIT. Benchmark alignment remains unverified.
- **Product reference:** Apache Tomcat 9 documentation, https://tomcat.apache.org/tomcat-9.0-doc/.
- **Validation status:** UNTESTED means not yet lab/idempotency/authoritative-assessment verified after this reconciliation.

For **INHERITED/ADAPTED** rows, the material used is the implementation from the supplied v0.3 baseline, reconciled to current V3R4 semantics where changes were identified. For **ORIGINAL** rows, the implementation was written in this review directly from current V3R4 check/fix semantics, with Apache product documentation used only to confirm Tomcat behavior. Public Ansible-Lockdown code was not established as a material source for these implementations.

## Per-control provenance/coverage ledger

| V-ID | Implementation type | Provenance | Source basis | Coverage | Test risk | Validation status |
|---|---|---|---|---|---|---|
| V-222931 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222964 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222965 | REMEDIATION | ORIGINAL | Current V3R4 + Apache Tomcat product docs as applicable | PRESENT | HIGH | UNTESTED |
| V-222968 | REMEDIATION/EVIDENCE | ORIGINAL | Current V3R4 + Apache Tomcat product docs as applicable | PRESENT-MIXED | HIGH | UNTESTED |
| V-222930 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222932 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222933 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222934 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222935 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222937 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222938 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222939 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222940 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222942 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222943 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222944 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222945 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222946 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222947 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222948 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222949 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222950 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222951 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222952 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222955 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222956 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222961 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222962 | REMEDIATION | ORIGINAL | Current V3R4 + Apache Tomcat product docs as applicable | PRESENT | HIGH | UNTESTED |
| V-222963 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222966 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222967 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222969 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222970 | REMEDIATION | ORIGINAL | Current V3R4 + Apache Tomcat product docs as applicable | PRESENT | HIGH | UNTESTED |
| V-222971 | REMEDIATION/EVIDENCE | ORIGINAL | Current V3R4 + Apache Tomcat product docs as applicable | PRESENT-MIXED | HIGH | UNTESTED |
| V-222974 | AUDIT/EVIDENCE | ORIGINAL | Current V3R4 + Apache Tomcat product docs as applicable | PRESENT-MIXED | HIGH | UNTESTED |
| V-222975 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222977 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222979 | REMEDIATION | ORIGINAL | Current V3R4 + Apache Tomcat product docs as applicable | PRESENT | HIGH | UNTESTED |
| V-222980 | REMEDIATION | ORIGINAL | Current V3R4 + Apache Tomcat product docs as applicable | PRESENT | HIGH | UNTESTED |
| V-222981 | REMEDIATION | ORIGINAL | Current V3R4 + Apache Tomcat product docs as applicable | PRESENT | HIGH | UNTESTED |
| V-222983 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222984 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222986 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222987 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222988 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222991 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222993 | AUDIT/EVIDENCE | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222994 | AUDIT/EVIDENCE | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222995 | AUDIT/EVIDENCE | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222996 | AUDIT/EVIDENCE | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222997 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222998 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222999 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-223000 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-223004 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-223005 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-223006 | EVIDENCE | ORIGINAL | Current V3R4 + Apache Tomcat product docs as applicable | PRESENT-MIXED | HIGH | UNTESTED |
| V-223010 | AUDIT/EVIDENCE | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222926 | REMEDIATION | ORIGINAL | Current V3R4 + Apache Tomcat product docs as applicable | PRESENT | HIGH | UNTESTED |
| V-222928 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222941 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222953 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222954 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222957 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222958 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222959 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222960 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222973 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222976 | REMEDIATION | ORIGINAL | Current V3R4 + Apache Tomcat product docs as applicable | PRESENT | HIGH | UNTESTED |
| V-222982 | REMEDIATION | ORIGINAL | Current V3R4 + Apache Tomcat product docs as applicable | PRESENT | HIGH | UNTESTED |
| V-222985 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222989 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-222990 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-223001 | AUDIT/EVIDENCE | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-223002 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-223003 | REMEDIATION/AUDIT | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-223007 | AUDIT/EVIDENCE | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-223008 | AUDIT/EVIDENCE | INHERITED/ADAPTED | Internal v0.3 baseline + current V3R4 reconciliation | PRESENT | HIGH | UNTESTED |
| V-223009 | REMEDIATION | ORIGINAL | Current V3R4 + Apache Tomcat product docs as applicable | PRESENT | HIGH | UNTESTED |

## Interpretation

- **INHERITED/ADAPTED** here means the repository implementation descends from the project-owner-supplied v0.3 baseline and has, in some cases, received later local corrections. It does **not** assert inheritance from any public repository.
- **ORIGINAL** on the controls corrected in this round means the implementation was created directly from the current V3R4 check/fix semantics during this provenance review; no public implementation was used as source code.
- **PRESENT-MIXED** means the repository now has the legitimate Tomcat-side remediation/audit behavior, but final compliance still depends on site-owned evidence or architecture.
- All controls remain HIGH first-cycle scrutiny until a compliant RHEL 8/9 baseline is demonstrated with authoritative V3R4 assessment results.
- Removed V3R3-era controls V-222927, V-222929, and V-222936 are not current V3R4 implementation targets.

## Validation status

No row should be described as assessment-verified merely because it is tagged in Ansible. Present controls still require syntax, lab, idempotency, functional, and authoritative-assessment validation. No current V3R4 control remains silently absent from the role. Deterministic and evidence-dependent controls still require syntax, lab, idempotency, functional, and authoritative-assessment validation before tester handoff.
