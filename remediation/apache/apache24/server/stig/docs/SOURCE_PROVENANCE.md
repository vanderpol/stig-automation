# Apache Server 2.4 UNIX Server STIG V3R3 - Retrospective Source Provenance

**Status:** retrospective reconstruction. The Apache implementation predates the repository provenance policy. This ledger records what can be established now and does not claim contemporaneous source tracking.

**Implementation authority:** current Server V3R3 DISA benchmark. Public implementations are comparison/reference material only. Historical STIG material is not implementation authority.

## Sources consulted

- Current DISA-derived Apache STIG check/fix text as exposed by current STIG reference sites.
- Ansible-Lockdown APACHE-2.4-STIG: public Apache remediation project used as a conceptual comparison/reference. During this retrospective review, indexed public material established the project and its scope, but did not provide reliable per-V-ID source-code evidence for every control. Therefore **no control is classified INHERITED solely because a similar task exists upstream**.
- Rocky Linux DISA Apache STIG documentation: secondary comparison material for technical-versus-operational treatment of several controls.
- Apache/Ansible conventional configuration techniques where noted as COMMON.

## Interpretation

- **COMMON** means the implementation is an obvious/direct Apache or Ansible technique and similar implementations are expected independently.
- **ADAPTED** means public/current guidance materially informed the approach, while our cross-distro/task logic is locally implemented.
- **ORIGINAL** means the first-pass implementation/audit design was developed locally from current requirement semantics and no specific upstream implementation was established as its source.
- No row below is presently classified **INHERITED** because this retrospective review did not establish line-level or task-level copying sufficient to make that claim. If repository history later establishes direct inheritance, update the row and attribution.

## Per-control ledger

| V-ID | Implementation type | Provenance | Test scrutiny | Retrospective basis |
|---|---|---|---|---|
| V-214228 | AUTO-VAR | ORIGINAL | HIGH | Site-defined concurrency/operational tuning; no public implementation was established as the source. |
| V-214229 | APP/EVIDENCE | ORIGINAL | HIGH | Application session behavior; local evidence boundary. |
| V-214230 | AUTO-VAR | COMMON | HIGH | TLS hardening is common, but local cross-distro module/package and directive handling is new. |
| V-214231 | AUTO | COMMON | MEDIUM | Standard Apache logging configuration. |
| V-214232 | AUTO | COMMON | MEDIUM | Standard Apache access/startup/auth logging concepts. |
| V-214233 | AUTO-VAR | ORIGINAL | HIGH | Proxy/load-balancer client-IP handling requires site-specific architecture. |
| V-214234 | EVIDENCE | ORIGINAL | HIGH | Operational alerting evidence, not deterministic Apache remediation. |
| V-214235 | AUTO | COMMON | MEDIUM | Conventional log-file permission hardening. |
| V-214236 | AUTO | COMMON | MEDIUM | Conventional log ownership/permission hardening. |
| V-214237 | EVIDENCE | ORIGINAL | HIGH | Backup architecture/process evidence. |
| V-214238 | EVIDENCE | ORIGINAL | HIGH | Module review/testing/signature evidence. |
| V-214239 | APP | ORIGINAL | HIGH | Hosted-application user-management boundary. |
| V-214240 | EVIDENCE | ORIGINAL | HIGH | Necessary-services determination is site/mission dependent. |
| V-214241 | AUTO-VAR | COMMON | MEDIUM | ProxyRequests Off is a conventional Apache hardening control; authorization remains site-owned. |
| V-214242 | AUTO | COMMON | MEDIUM | Removal of Apache documentation package is a common hardening technique and is also described in public Rocky Linux STIG guidance. |
| V-214243 | AUTO-VAR | ADAPTED | HIGH | Common FilesMatch/deny technique, but local configurable extension regex and cross-distro implementation require focused testing. |
| V-214244 | AUTO-VAR | ADAPTED | HIGH | Public guidance describes removal of unused Script/ScriptAlias/CGI mappings; local module-oriented implementation differs and overlaps Site V-214282. |
| V-214245 | AUTO | ADAPTED | HIGH | Public STIG guidance disables DAV modules; local implementation adds Ubuntu a2dismod and RHEL config discovery. |
| V-214246 | AUTO-VAR | ADAPTED | HIGH | Public guidance requires explicit IP/port; local implementation rewrites unmanaged Listen directives and is therefore higher risk. |
| V-214247 | AUDIT-VAR | ORIGINAL | HIGH | Local ownership discovery against site-approved admin accounts. |
| V-214248 | AUDIT-VAR | ORIGINAL | HIGH | Local privileged-path metadata audit. |
| V-214249 | EVIDENCE | ORIGINAL | HIGH | Management/application separation architecture evidence. |
| V-214250 | APP/EVIDENCE | ORIGINAL | HIGH | Application session invalidation behavior. |
| V-214251 | APP/EVIDENCE | ORIGINAL | HIGH | Application cookie scope/security behavior. |
| V-214252 | APP/EVIDENCE | ORIGINAL | HIGH | Application session-ID strength evidence. |
| V-214253 | AUTO | ADAPTED | HIGH | Current STIG explicitly checks unique_id_module; local RHEL/Ubuntu enablement is newly implemented. |
| V-214254 | EVIDENCE | ORIGINAL | HIGH | Safe-state behavior requires architecture/application evidence. |
| V-214255 | AUTO | COMMON | MEDIUM | Direct current-STIG mapping to Timeout <=60; simple directive. |
| V-214256 | AUTO | ORIGINAL | HIGH | Comparison exposed a first-pass gap: current check requires ErrorDocument handling. Local remediation was corrected during provenance review with sanitized 401/403/404/500 ErrorDocument directives; lab/assessment validation remains required. |
| V-214257 | AUTO | COMMON | MEDIUM | TraceEnable/LogLevel hardening uses standard Apache directives. |
| V-214258 | AUDIT-VAR | ORIGINAL | HIGH | Application categorization determines timeout. |
| V-214259 | AUTO-VAR | ORIGINAL | HIGH | Organization-defined network-zone enforcement; prior global enforcement was intentionally removed pending exact safe scoping. |
| V-214260 | EVIDENCE | ORIGINAL | HIGH | Emergency disconnect capability is operational evidence. |
| V-214261 | AUDIT-VAR | ORIGINAL | HIGH | Local distinct-admin-account audit logic. |
| V-214262 | EVIDENCE | ORIGINAL | HIGH | Capacity planning evidence. |
| V-214263 | EVIDENCE | ORIGINAL | HIGH | Remote audit logging architecture evidence. |
| V-214264 | EVIDENCE | ORIGINAL | HIGH | Security-infrastructure integration evidence. |
| V-214265 | AUTO/EVIDENCE | ORIGINAL | HIGH | Timestamp/time-source semantics need authoritative assessment validation. |
| V-214267 | AUTO | COMMON | HIGH | File/PID/control protection is conventional but local path handling spans distros. |
| V-214268 | APP | ORIGINAL | HIGH | HttpOnly behavior is application/site-sensitive; global mutation was removed from first-pass remediation. |
| V-214269 | AUTO-VAR | ADAPTED | HIGH | Current STIG requires !EXPORT/!EXP in every enabled cipher directive; local scan/replace across config files is new logic. |
| V-214270 | EVIDENCE | ORIGINAL | HIGH | Patch timeliness requires vendor/package/process evidence. |
| V-214271 | AUTO | COMMON | MEDIUM | Conventional non-login service-account hardening. |
| V-214273 | EVIDENCE | ORIGINAL | HIGH | Vendor-support status is evidence, especially with distro backports. |
| V-214274 | AUTO | ADAPTED | HIGH | Current STIG has specific htpasswd ownership/access semantics; local recursive discovery and permission choice require assessment validation. |

## Validation status

All rows are currently **first-pass / lab-validation pending** unless a later test record explicitly says otherwise. HIGH scrutiny means syntax/config validation, positive remediation, idempotency, authoritative assessment comparison, application/service functional testing, and a deliberate edge/negative case should be emphasized. Future Anti-STIG coverage should prioritize these HIGH rows after a compliant baseline is established.
