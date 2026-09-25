# Apache 2.4 Provenance Comparison Summary

## Scope

Retrospective provenance review completed for all **61 current controls**:
- Server V3R3: 45 controls.
- Site V2R7: 16 controls.

This is explicitly retrospective because the Apache implementation began before the repository provenance policy was adopted.

## Comparison sources

Primary implementation authority remains the current DISA benchmark.

Public comparison/reference material included:
- Ansible-Lockdown APACHE-2.4-STIG, a maintained public Apache STIG remediation project.
- Rocky Linux DISA Apache STIG documentation.
- Current DISA-derived check/fix text available through current STIG reference sites.
- Conventional Apache/Ansible configuration patterns.

The review did **not** classify code as inherited merely because another role uses the same Apache directive. Indexed public material did not establish reliable line-level/task-level ancestry for every V-ID, so there are currently no controls marked INHERITED. This avoids inventing provenance after the fact.

## Classification counts

| Provenance | Server | Site | Total |
|---|---:|---:|---:|
| COMMON | 11 | 2 | 13 |
| ADAPTED | 7 | 3 | 10 |
| ORIGINAL | 5 | 1 | 6 |
| EVIDENCE/AUDIT | 22 | 10 | 32 |
| INHERITED | 0 | 0 | 0 |
| **Total** | **45** | **16** | **61** |

These categories describe implementation provenance, not ownership of the STIG requirement.

## Test-risk result

The retrospective review intentionally assigns HIGH scrutiny to newly written cross-distro logic, config-file mutation, regex/module handling, organization-defined controls, and evidence/audit logic that could influence an assessment conclusion.

Approximate first-cycle priority:
- Server: 36 HIGH, 9 MEDIUM.
- Site: 15 HIGH, 1 MEDIUM.
- Combined: **51 HIGH, 10 MEDIUM**.

No control is BASELINE yet because this first-pass implementation has not established a repeated assessment-verified history on the supported platform matrix.

## Important findings from the comparison

### Server V-214256

The comparison found a real first-pass implementation gap. The current check requires sanitized/custom `ErrorDocument` handling; ServerTokens/ServerSignature alone are not sufficient. The role was corrected during this provenance review to add sanitized 401/403/404/500 ErrorDocument directives. This correction is HIGH scrutiny until lab and authoritative assessment validation.

### Site V-214292

The comparison found that `Options -Indexes` is useful defense-in-depth but does **not** by itself satisfy the current check. The current check expects an `index.html` or equivalent default document in applicable document-root directories. The control matrix is therefore changed to AUDIT-VAR and the existing -Indexes setting must not be interpreted as proof of compliance.

### Site V-214290

Current check semantics confirm that the document root must be on a different filesystem/partition from both OS and Apache system files. Existing `findmnt` discovery is useful but needs assessment comparison logic; this remains HIGH scrutiny.

### Server V-214244 / Site V-214282

The existing cross-benchmark duplicate candidate remains. Both current V-IDs are retained. The underlying script-mapping behavior should be tested once technically while both assessment identities remain independently traceable.

## What “ADAPTED” means here

ADAPTED does not mean copied source code. In this retrospective ledger it means public/current guidance materially informed the implementation approach, while the repository's RHEL/Ubuntu abstraction, safety boundaries, variables, audit behavior, or task logic are locally implemented.

Examples include DAV module disabling, explicit Listen enforcement, cipher exclusion, script-mapping handling, and cookie/header handling.

## What to test first

Highest-value first-cycle scrutiny should concentrate on:
1. controls corrected or reclassified by this comparison (V-214256, V-214292);
2. cross-file/config mutation (V-214246, V-214269);
3. distro-specific module behavior (V-214245, V-214253);
4. filesystem/site-content semantics (V-214290, V-214292);
5. cookie/application behavior (V-214303 and evidence-oriented cookie/session controls);
6. authorization/account audits;
7. any control whose PASS depends on evidence rather than a deterministic Apache directive.

The detailed per-V-ID rationale is in the Server and Site SOURCE_PROVENANCE.md ledgers.
