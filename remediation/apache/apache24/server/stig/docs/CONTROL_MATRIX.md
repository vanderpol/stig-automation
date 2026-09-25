# Apache Server 2.4 UNIX Server STIG V3R3 control matrix

Benchmark: V3R3, released 2026-05-28. 45 findings: 5 CAT I, 40 CAT II.

Classification policy: AUTO means the STIG check/fix can be deterministically enforced without inventing site policy. AUTO-VAR requires an explicit site-approved value. EVIDENCE requires architecture, process, authorization, or other evidence. APP means the requirement belongs primarily to the hosted application/site and must not be falsely claimed by the server role.

| V-ID | Class | Requirement summary |
|---|---|---|
| V-214228 | AUTO-VAR | Limit simultaneous session requests |
| V-214229 | APP/EVIDENCE | Server-side session management |
| V-214230 | AUTO-VAR | Cryptographic protection of remote sessions |
| V-214231 | AUTO | System logging enabled |
| V-214232 | AUTO | Startup/shutdown/access/authentication logging |
| V-214233 | AUTO-VAR | Preserve client IP behind proxy/load balancer |
| V-214234 | EVIDENCE | Alert on log processing failure |
| V-214235 | AUTO | Restrict log-file access |
| V-214236 | AUTO | Protect logs from modification/deletion |
| V-214237 | EVIDENCE | Back up logs to different system/media |
| V-214238 | EVIDENCE | Review/test/sign expansion modules |
| V-214239 | APP | No user management for hosted applications |
| V-214240 | EVIDENCE | Only necessary services/functions |
| V-214241 | AUTO-VAR | Must not act as proxy unless explicitly required/authorized |
| V-214242 | AUTO | Exclude/remove docs, samples, examples, tutorials |
| V-214243 | AUTO-VAR | Disable serving prohibited file types |
| V-214244 | AUTO-VAR | Remove unused/vulnerable script mappings |
| V-214245 | AUTO | Disable WebDAV |
| V-214246 | AUTO-VAR | Bind specified IP address and port |
| V-214247 | AUDIT-VAR | Administrative accounts only for OS/directory-tree access |
| V-214248 | AUDIT-VAR | Privileged access to app dirs/libraries/config |
| V-214249 | EVIDENCE | Separate hosted apps from management |
| V-214250 | APP/EVIDENCE | Invalidate session IDs at termination |
| V-214251 | APP/EVIDENCE | Cookie scope/security |
| V-214252 | APP/EVIDENCE | Session ID >=128-bit strength |
| V-214253 | AUTO | Session ID character-space strength |
| V-214254 | EVIDENCE | Fail to known safe state |
| V-214255 | AUTO | Timeout <=60 seconds / operational tuning |
| V-214256 | AUTO | Minimize server identity in errors |
| V-214257 | AUTO | Disable debugging/trace |
| V-214258 | AUDIT-VAR | Inactive session timeout |
| V-214259 | AUTO-VAR | Restrict inbound nonsecure zones |
| V-214260 | EVIDENCE | Immediate remote-access disconnect capability |
| V-214261 | AUDIT-VAR | Distinct administrative account for security functions |
| V-214262 | EVIDENCE | Adequate log storage capacity |
| V-214263 | EVIDENCE | Do not impede remote audit logging |
| V-214264 | EVIDENCE | Integrate with organization security infrastructure |
| V-214265 | AUTO/EVIDENCE | Log timestamps map to UTC/GMT, >=1-second granularity |
| V-214267 | AUTO | Nonprivileged users cannot stop Apache |
| V-214268 | APP | HttpOnly cookie behavior |
| V-214269 | AUTO-VAR | Remove export/weak ciphers |
| V-214270 | EVIDENCE | Timely security updates |
| V-214271 | AUTO | Service account has no valid login shell/password |
| V-214273 | EVIDENCE | Vendor-supported Apache version |
| V-214274 | AUTO | Proper htpasswd ownership/permissions |

This matrix is the implementation ledger. A control is not promoted to AUTO merely because a plausible hardening directive exists.

## Administrative-boundary policy

V-214247, V-214248, and V-214261 are intentionally non-destructive. The STIG relies on environment-defined administrative roles/accounts and privileged access boundaries. The role may discover and compare ownership/access against explicit site inputs, but it must not invent an administrative service account or recursively rewrite ownership to manufacture compliance.

Suggested inputs:
- `apache24_stig_approved_admin_accounts`
- `apache24_stig_admin_audit_paths`
- `apache24_stig_privileged_paths`

A reported match supports assessment; authorization of those accounts remains site evidence.

## Session-control note

V-214253 is server-remediable in the current benchmark check: compliance is determined by whether Apache's `unique_id_module` is loaded. The role therefore enables `mod_unique_id` rather than treating the rule as purely application evidence.

V-214229, V-214250, V-214251, and V-214252 depend on hosted-application/session behavior and are retained as evidence-oriented checks. V-214258 requires application categorization before selecting the STIG timeout value (5/10/20 minutes), so the role validates a supplied value but does not invent the categorization.
