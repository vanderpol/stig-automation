# Apache Server 2.4 UNIX Site STIG V2R7 - Retrospective Source Provenance

**Status:** retrospective reconstruction. The Site implementation predates the repository provenance policy.

**Implementation authority:** current Site V2R7 DISA benchmark. Public implementations are comparison/reference material only; older STIG releases are not implementation authority.

## Sources consulted

- Current DISA-derived Site V2R7 check/fix material through current STIG reference sites.
- Ansible-Lockdown APACHE-2.4-STIG as a public conceptual comparison/reference. Indexed material confirms a maintained Apache STIG remediation project, but this retrospective review did not establish reliable per-V-ID source-code provenance for all Site controls.
- Rocky Linux Apache STIG documentation as secondary comparison material.
- Conventional Apache configuration behavior for controls classified COMMON.

## Attribution rule used in this reconstruction

Similarity is not inheritance. No Site row is classified INHERITED without evidence that our task/code was materially copied from a particular upstream task. ADAPTED records conceptual/source influence plus local implementation. ORIGINAL records locally developed implementation where no specific upstream implementation was established. EVIDENCE/AUDIT identifies locally designed assessment/evidence handling.

## Per-control ledger

| V-ID | Impl class | Provenance | Test scrutiny | Retrospective basis |
|---|---|---|---|---|
| V-214280 | APP/EVIDENCE | EVIDENCE/AUDIT | HIGH | Application user-management architecture; no safe deterministic server fix. |
| V-214282 | AUTO-VAR | ADAPTED | HIGH | Same current requirement theme as Server V-214244; public guidance covers unused script mappings, while local Site treatment preserves separate V-ID traceability. |
| V-214284 | AUTO-VAR | ADAPTED | HIGH | Directory containment uses common Apache Directory/Options controls; local site-profile scoping is new. |
| V-214286 | EVIDENCE | EVIDENCE/AUDIT | HIGH | RFC 5280 path-validation evidence is site/PKI architecture dependent. |
| V-214287 | AUDIT-VAR | EVIDENCE/AUDIT | HIGH | Local private-key ownership/mode inspection against organization-approved administrators/PKI Sponsor. |
| V-214288 | APP/AUDIT-VAR | EVIDENCE/AUDIT | HIGH | Cookie Domain/Path behavior belongs to application/site design. |
| V-214289 | EVIDENCE | EVIDENCE/AUDIT | HIGH | Stable-baseline/recovery capability is process/evidence. |
| V-214290 | AUDIT-VAR | ORIGINAL | HIGH | Local findmnt-based filesystem discovery was created for the current requirement; still needs comparison of document-root filesystem to Apache system/config filesystem. |
| V-214292 | AUTO-VAR | COMMON | HIGH | Comparison found that -Indexes is useful hardening but does not itself satisfy the current check, which requires index.html or equivalent default content in each applicable directory. Treat current remediation as partial pending site-content audit/assessment. |
| V-214296 | APP/AUDIT-VAR | EVIDENCE/AUDIT | HIGH | Inactive timeout is application/category dependent. |
| V-214297 | AUTO-VAR | EVIDENCE/AUDIT | HIGH | Organization-defined network zones may be enforced outside Apache; unsafe global Require logic was deliberately removed. |
| V-214298 | AUDIT-VAR | EVIDENCE/AUDIT | HIGH | Distinct administrative-account boundary is organization-defined. |
| V-214300 | EVIDENCE | EVIDENCE/AUDIT | HIGH | DoD/DoD-approved client CA authorization cannot be inferred from a CA file. |
| V-214301 | AUTO | COMMON | MEDIUM | SSLCompression Off is a direct/common Apache TLS directive. |
| V-214303 | APP/AUTO-VAR | ADAPTED | HIGH | Secure-cookie enforcement uses a common headers technique, but global response-cookie mutation can affect applications and requires functional testing. |
| V-214304 | AUDIT-VAR | EVIDENCE/AUDIT | HIGH | Ports/protocols/modules/services require approved-use/PPSM context. |

## Validation status

All rows remain **first-pass / lab-validation pending** unless later test records explicitly establish otherwise. HIGH-risk Site controls deserve particular functional testing because application behavior, PKI, authorization, filesystem layout, cookies, sessions, and network policy can make a syntactically valid Apache configuration operationally wrong.

## Cross-benchmark duplicate candidate

Server V-214244 and Site V-214282 remain separate current findings. They share the unused/vulnerable script-mapping requirement theme and should be tested for one underlying configuration outcome while retaining both assessment identities.
