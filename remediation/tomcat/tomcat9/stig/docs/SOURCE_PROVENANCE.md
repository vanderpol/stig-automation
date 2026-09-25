# Apache Tomcat 9 V3R4 - Retrospective Source Provenance

**Status:** retrospective reconstruction. The Tomcat role predates the repository provenance policy.

**Current authority:** Apache Tomcat Application Server 9 STIG V3R4, 79 findings. Current-check comparison was performed against V3R4 reference material. Historical releases are not implementation authority.

## Source lineage established

1. The repository README explicitly identifies the project-owner-supplied `tomcat9_stig_ansible_rhel8_rhel9_v0.3` project as the implementation baseline. Existing v0.3-derived tasks are therefore classified **INHERITED (internal project baseline)** where no later substantial redesign is known.
2. Subsequent repository reconciliation changed several inherited tasks (service-account UID handling, audit package installation, truststore password handling, XML namespace handling, booleans, path discovery, and tester UX). Those changes are local adaptations on top of the inherited baseline.
3. Ansible-Lockdown maintains a public TOMCAT-9-STIG remediation project and was consulted during this retrospective comparison as a public reference. This review did **not** establish that the project-owner v0.3 baseline was copied from Ansible-Lockdown. Upstream ancestry of v0.3 remains **unresolved** unless earlier development records establish it.
4. Apache Tomcat community review material was consulted as technical commentary because it identifies semantic/operability concerns in the DISA Tomcat STIG; it is not implementation authority.

## Important finding

The previous control matrix stated 79 findings and classification totals, but executable task/tag reconciliation shows **14 current V3R4 controls with missing or partial implementation/audit coverage**. Provenance review therefore found a substantive coverage issue, not just an attribution issue.

## Per-control provenance/coverage ledger

| V-ID | Implementation type | Provenance | Coverage | Test risk |
|---|---|---|---|---|
| V-222931 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222964 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222965 | REVIEW/TO-IMPLEMENT | ORIGINAL-PENDING | GAP | HIGH |
| V-222968 | REVIEW/TO-IMPLEMENT | ORIGINAL-PENDING | GAP | HIGH |
| V-222930 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222932 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222933 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222934 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222935 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222937 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222938 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222939 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222940 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222942 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222943 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222944 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222945 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222946 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222947 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222948 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222949 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222950 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222951 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222952 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222955 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222956 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222961 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222962 | REVIEW/TO-IMPLEMENT | ORIGINAL-PENDING | GAP | HIGH |
| V-222963 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222966 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222967 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222969 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222970 | REVIEW/TO-IMPLEMENT | ORIGINAL-PENDING | GAP | HIGH |
| V-222971 | REVIEW/TO-IMPLEMENT | ORIGINAL-PENDING | GAP | HIGH |
| V-222974 | REVIEW/TO-IMPLEMENT | ORIGINAL-PENDING | GAP | HIGH |
| V-222975 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222977 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222979 | REVIEW/TO-IMPLEMENT | ORIGINAL-PENDING | GAP | HIGH |
| V-222980 | REVIEW/TO-IMPLEMENT | ORIGINAL-PENDING | GAP | HIGH |
| V-222981 | REVIEW/TO-IMPLEMENT | ORIGINAL-PENDING | GAP | HIGH |
| V-222983 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222984 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222986 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222987 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222988 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222991 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222993 | AUDIT/EVIDENCE | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222994 | AUDIT/EVIDENCE | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222995 | AUDIT/EVIDENCE | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222996 | AUDIT/EVIDENCE | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222997 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222998 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222999 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-223000 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-223004 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-223005 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-223006 | REVIEW/TO-IMPLEMENT | ORIGINAL-PENDING | GAP | HIGH |
| V-223010 | AUDIT/EVIDENCE | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222926 | REVIEW/TO-IMPLEMENT | ORIGINAL-PENDING | GAP | HIGH |
| V-222928 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222941 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222953 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222954 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222957 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222958 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222959 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222960 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222973 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222976 | REVIEW/TO-IMPLEMENT | ORIGINAL-PENDING | GAP | HIGH |
| V-222982 | REVIEW/TO-IMPLEMENT | ORIGINAL-PENDING | GAP | HIGH |
| V-222985 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222989 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222990 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-223001 | AUDIT/EVIDENCE | INHERITED/ADAPTED | PRESENT | HIGH |
| V-223002 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-223003 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-223007 | AUDIT/EVIDENCE | INHERITED/ADAPTED | PRESENT | HIGH |
| V-223008 | AUDIT/EVIDENCE | INHERITED/ADAPTED | PRESENT | HIGH |
| V-223009 | REVIEW/TO-IMPLEMENT | ORIGINAL-PENDING | PARTIAL | HIGH |

## Interpretation

- **INHERITED/ADAPTED** here means the repository implementation descends from the project-owner-supplied v0.3 baseline and has, in some cases, received later local corrections. It does **not** assert inheritance from any public repository.
- **ORIGINAL-PENDING** means the current V3R4 requirement has no executable implementation in the reconciled role yet; when implemented, its actual source lineage must be recorded contemporaneously.
- All controls remain HIGH first-cycle scrutiny until a compliant RHEL 8/9 baseline is demonstrated with authoritative V3R4 assessment results.
- Removed V3R3-era controls V-222927, V-222929, and V-222936 are not current V3R4 implementation targets.

## Validation status

No row should be described as assessment-verified merely because it is tagged in Ansible. Present controls still require syntax, lab, idempotency, functional, and authoritative-assessment validation. GAP/PARTIAL rows must be closed before the Tomcat role can claim all-current-control first-pass coverage.
