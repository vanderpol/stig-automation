# AGENTS.md

## Purpose

This repository automates DISA STIG remediation, audit/evidence handling, SCAP/OVAL validation, and later Anti-STIG regression testing.

Any agent, contributor, or automation working in this repository must optimize for **current-benchmark correctness, explicit provenance, conservative remediation, minimal blast radius, and testability**.

## Repository rules

1. **The current DISA benchmark is the implementation authority.**
   - Establish the exact STIG title, version, release, and publication date before implementation.
   - Historical releases may be used for change analysis only.
   - Never reintroduce a removed V-ID merely because older automation contains it.

2. **Enumerate the complete current V-ID set before implementation.**
   - Maintain a control matrix from the beginning.
   - Every current V-ID must end the first pass as one of: remediation, guarded remediation, audit, evidence, application-owned/evidence, or legitimate N/A/site-owned behavior.
   - No current control may silently disappear from code or documentation.

3. **Maintain provenance while work is performed.**
   - Follow `docs/PROVENANCE_POLICY.md`.
   - Do not reconstruct source history after implementation unless the work predates this policy.
   - Record exact source version/tag/commit/file/location and license when another implementation materially influences the result.

4. **Keep three dimensions separate.**
   - Provenance: `ORIGINAL | COMMON | ADAPTED | INHERITED | NEW-CURRENT`
   - Implementation type: `REMEDIATION | AUDIT | EVIDENCE | APP/EVIDENCE` or a justified mixed form.
   - Test risk: `HIGH | MEDIUM | BASELINE`
   - Never use implementation type as a provenance label.

5. **Treat public lockdown projects as references until freshness is proven.**
   Before materially using another project:
   - identify the STIG release it targets;
   - determine whether it was updated after the current benchmark publication date;
   - record exact source location and license;
   - compare its V-ID set against the current benchmark;
   - do not inherit obsolete controls or platform assumptions.
   A repository being labeled “maintained” is not sufficient evidence that it implements the current STIG release.

6. **A plausible hardening setting is not automatically the STIG requirement.**
   - Compare every implementation to the literal current DISA check and fix text.
   - Verify that the configuration file/path inspected by the current check is actually the path being remediated.
   - Equivalent product behavior in a different location may still fail the current assessment.

7. **Also verify product semantics.**
   - Use current vendor/product documentation to confirm directive names, attribute syntax, locations, inheritance, and side effects.
   - If current DISA wording conflicts with valid product syntax, document the discrepancy and implement product-valid behavior. Do not knowingly create invalid configuration merely to mimic erroneous wording.
   - Preserve exact assessment evidence so benchmark/tool discrepancies can be reconciled later.

8. **Never invent organization/site decisions.**
   Do not fabricate:
   - SSP/ISSO/ISSM approvals;
   - PKI trust anchors or CA approval;
   - network zones or approved interfaces;
   - privileged/admin accounts;
   - application/session architecture;
   - PPSM/RMF decisions;
   - HA/DR requirements;
   - patch/vendor-support evidence;
   - secrets, LDAP schema, cluster keys, or similar environment-specific values.
   Require explicit inputs/evidence or stop with a useful error.

9. **Minimize blast radius.**
   - Scope changes to the component named by the requirement whenever possible.
   - Do not rewrite unrelated applications, connectors, virtual hosts, realms, modules, or files simply because a broad change is easier.
   - Architecture-changing or potentially destructive remediation requires an explicit opt-in and clear documentation of side effects.

10. **Mandatory controls must not be silently disabled by defaults.**
    - Especially for CAT I findings, a false/empty default must not allow remediation to complete while knowingly leaving the requirement unmet.
    - Use a hard prerequisite or explicit evidence/guardrail where deterministic remediation cannot legitimately establish compliance.

11. **Current-check anomalies are documented, not silently interpreted away.**
    - Record inconsistent paths, filenames, syntax, or check/fix wording.
    - Follow current benchmark intent while preserving product-valid configuration.
    - Flag anomalies for testers and future benchmark reconciliation.

12. **New or substantially changed logic gets elevated scrutiny.**
    HIGH-risk examples include:
    - original current-release implementations;
    - regex/XML/parser/config-tree changes;
    - cross-file mutations;
    - platform-specific path logic;
    - authentication/PKI/crypto/network changes;
    - evidence/audit logic that can affect PASS/FAIL conclusions.

13. **Testing sequence**
    For a new lockdown or substantial update, the normal validation sequence is:
    1. preflight/discovery;
    2. check/diff review where meaningful;
    3. apply remediation;
    4. service/configuration validation;
    5. application/functional testing;
    6. second apply/idempotency;
    7. authoritative current STIG assessment;
    8. reconcile every unexpected V-ID;
    9. update provenance and test-risk records from findings.

14. **Do not call automation STIG-compliant because Ansible completed successfully.**
    Compliance requires authoritative assessment plus applicable organization/application evidence.

15. **Anti-STIG comes after a known-good compliant baseline.**
    - Do not build Anti-STIG first.
    - Once a control is assessment-verified, create deterministic fail -> remediate -> pass regression coverage where practical.

## New-lockdown workflow

Use this sequence for every new technology or major benchmark port:

`benchmark identification -> current V-ID enumeration -> provenance/source review -> public implementation freshness check -> control classification -> implementation -> literal current-check reconciliation -> product-documentation reconciliation -> blast-radius/risk review -> tester documentation -> lab validation -> authoritative assessment reconciliation -> Anti-STIG`

## Required artifacts for a substantial lockdown

At minimum, create or maintain:

- benchmark metadata;
- current control matrix;
- implementation code;
- provenance/source ledger;
- tester quick-start;
- test report/template;
- current-check anomaly notes when needed;
- first-pass/readiness status;
- Anti-STIG only after verified positive-baseline testing.

## Lessons learned

Read `docs/LOCKDOWN_LESSONS_LEARNED.md` before starting a new lockdown or major benchmark update. It captures the Apache and Tomcat failures and corrections that led to these rules.
