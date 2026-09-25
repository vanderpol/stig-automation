# Apache Tomcat 9 V3R4 - Retrospective Source Provenance

**Status:** retrospective reconstruction. The Tomcat role predates the repository provenance policy.

**Current authority:** Apache Tomcat Application Server 9 STIG V3R4, 79 findings. Current-check comparison was performed against V3R4 reference material. Historical releases are not implementation authority.

## Source lineage established

1. The repository README explicitly identifies the project-owner-supplied `tomcat9_stig_ansible_rhel8_rhel9_v0.3` project as the implementation baseline. Existing v0.3-derived tasks are therefore classified **INHERITED (internal project baseline)** where no later substantial redesign is known.
2. Subsequent repository reconciliation changed several inherited tasks (service-account UID handling, audit package installation, truststore password handling, XML namespace handling, booleans, path discovery, and tester UX). Those changes are local adaptations on top of the inherited baseline.
3. Ansible-Lockdown maintains a public TOMCAT-9-STIG remediation project. Its current public documentation still marks the role as maintained and remediation-capable, but the documentation does not expose the target DISA Tomcat STIG version or a reliable source-update date. Because the current DISA V3R4 benchmark is dated 2026-02-25, this review treats Ansible-Lockdown as **version alignment unverified** rather than assuming it is V3R4. No public-repository inheritance is asserted.
4. Apache Tomcat community review material was consulted as technical commentary because it identifies semantic/operability concerns in the DISA Tomcat STIG; it is not implementation authority.

## Important finding

The initial reconciliation found **14 current V3R4 controls with missing or partial implementation/audit coverage**. This round closed the deterministic gaps where safe and converted the remaining architecture/process items into explicit evidence/guardrail controls. The review therefore found and corrected substantive coverage issues, not just attribution issues.

## Per-control provenance/coverage ledger

| V-ID | Implementation type | Provenance | Coverage | Test risk |
|---|---|---|---|---|
| V-222931 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222964 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222965 | REMEDIATION | ORIGINAL | PRESENT | HIGH |
| V-222968 | REMEDIATION/EVIDENCE | ORIGINAL | PRESENT-MIXED | HIGH |
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
| V-222962 | REMEDIATION | ORIGINAL | PRESENT | HIGH |
| V-222963 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222966 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222967 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222969 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222970 | REMEDIATION | ORIGINAL | PRESENT | HIGH |
| V-222971 | AUDIT/EVIDENCE | ORIGINAL | PRESENT-MIXED | HIGH |
| V-222974 | AUDIT/EVIDENCE | ORIGINAL | PRESENT-MIXED | HIGH |
| V-222975 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222977 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222979 | REMEDIATION | ORIGINAL | PRESENT | HIGH |
| V-222980 | REMEDIATION | ORIGINAL | PRESENT | HIGH |
| V-222981 | REMEDIATION | ORIGINAL | PRESENT | HIGH |
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
| V-223006 | EVIDENCE | ORIGINAL | PRESENT-MIXED | HIGH |
| V-223010 | AUDIT/EVIDENCE | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222926 | REMEDIATION | ORIGINAL | PRESENT | HIGH |
| V-222928 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222941 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222953 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222954 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222957 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222958 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222959 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222960 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222973 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222976 | REMEDIATION | ORIGINAL | PRESENT | HIGH |
| V-222982 | REMEDIATION | ORIGINAL | PRESENT | HIGH |
| V-222985 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222989 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-222990 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-223001 | AUDIT/EVIDENCE | INHERITED/ADAPTED | PRESENT | HIGH |
| V-223002 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-223003 | REMEDIATION/AUDIT | INHERITED/ADAPTED | PRESENT | HIGH |
| V-223007 | AUDIT/EVIDENCE | INHERITED/ADAPTED | PRESENT | HIGH |
| V-223008 | AUDIT/EVIDENCE | INHERITED/ADAPTED | PRESENT | HIGH |
| V-223009 | REMEDIATION | ORIGINAL | PRESENT | HIGH |

## Interpretation

- **INHERITED/ADAPTED** here means the repository implementation descends from the project-owner-supplied v0.3 baseline and has, in some cases, received later local corrections. It does **not** assert inheritance from any public repository.
- **ORIGINAL** on the controls corrected in this round means the implementation was created directly from the current V3R4 check/fix semantics during this provenance review; no public implementation was used as source code.
- **PRESENT-MIXED** means the repository now has the legitimate Tomcat-side remediation/audit behavior, but final compliance still depends on site-owned evidence or architecture.
- All controls remain HIGH first-cycle scrutiny until a compliant RHEL 8/9 baseline is demonstrated with authoritative V3R4 assessment results.
- Removed V3R3-era controls V-222927, V-222929, and V-222936 are not current V3R4 implementation targets.

## Validation status

No row should be described as assessment-verified merely because it is tagged in Ansible. Present controls still require syntax, lab, idempotency, functional, and authoritative-assessment validation. No current V3R4 control remains silently absent from the role. Deterministic and evidence-dependent controls still require syntax, lab, idempotency, functional, and authoritative-assessment validation before tester handoff.
