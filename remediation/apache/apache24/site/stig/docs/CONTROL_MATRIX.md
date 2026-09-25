# Apache Server 2.4 UNIX Site STIG V2R7 control matrix

Benchmark: V2R7, released 2026-05-23. 16 findings: 15 CAT II and 1 CAT III.

Classification policy matches the Server role: AUTO, AUTO-VAR, AUDIT-VAR, APP/EVIDENCE, and EVIDENCE.

| V-ID | Class | Requirement summary |
|---|---|---|
| V-214280 | APP/EVIDENCE | Apache must not perform hosted-application user management |
| V-214282 | AUTO-VAR | Remove unused/vulnerable script mappings |
| V-214284 | AUTO-VAR | Contain users/scripts to approved document/home tree |
| V-214286 | EVIDENCE | RFC 5280-compliant certification-path validation |
| V-214287 | AUDIT-VAR | Restrict private-key access to approved administrators/PKI Sponsor |
| V-214288 | APP/AUDIT-VAR | Cookie domain/path scope prevents cross-site/application access |
| V-214289 | EVIDENCE | Support re-creation from a stable known baseline |
| V-214290 | AUDIT-VAR | Document root resides on a separate partition/filesystem |
| V-214292 | AUTO-VAR | Prevent directory listing / provide default site page behavior |
| V-214296 | APP/AUDIT-VAR | Inactive session timeout |
| V-214297 | AUTO-VAR | Restrict inbound connections from organization-defined nonsecure zones |
| V-214298 | AUDIT-VAR | Distinct administrative account boundary |
| V-214300 | EVIDENCE | Accept only DoD PKI or DoD-approved client-certificate CAs |
| V-214301 | AUTO | Disable TLS compression |
| V-214303 | APP/AUTO-VAR | Force Secure property on cookies sent over TLS |
| V-214304 | AUDIT-VAR | Restrict unnecessary/nonsecure ports, protocols, modules and services |

## End-user boundary

The automation must not download trust anchors, designate approved CAs/accounts, manufacture authorization/PPSM approval, or claim that an evidence variable establishes compliance. It may inspect configuration facts and apply deterministic settings after the site supplies the authorization boundary.

V2R7 removed a number of historical Site controls; only the 16 V-IDs above belong in the current implementation.
