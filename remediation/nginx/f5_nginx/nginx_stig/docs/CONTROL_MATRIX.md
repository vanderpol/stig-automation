# F5 NGINX DISA STIG V1R1 — control/remediation matrix

Authority: **F5 NGINX Security Technical Implementation Guide V1R1**, benchmark date 2025-11-25 / public release listing 2026-01-07. The benchmark contains **32 findings: V-278380 through V-278411; 2 CAT I and 30 CAT II**.

Classification follows repository policy: `AUTO`, `AUTO-VAR`, `EXTERNAL+VAR`, `HUMAN/EVIDENCE`, `HUMAN/ARCH`, and `PROCESS`. First-pass status means represented in remediation/audit/evidence handling; it does not mean assessment-verified.

| V-ID | CAT | Short requirement | Class | First-pass treatment |
|---|---|---|---|---|
| V-278380 | II | concurrent sessions/worker connections | AUTO-VAR | SSP value required; worker_connections |
| V-278381 | I | TLS 1.2 minimum | AUTO | TLS 1.2/1.3 drop-in |
| V-278382 | II | service account no shell | AUTO | nologin shell |
| V-278383 | II | service account no admin group | AUTO | audit/removal of common privileged groups |
| V-278384 | II | DOD consent banner | HUMAN/ARCH | application-aware evidence required |
| V-278385 | II | auditable events/log fields | AUTO-VAR | effective custom log_format fields asserted |
| V-278386 | II | ISSM controls audit selection | AUTO | nginx.conf owner-write restriction |
| V-278387 | II | prevent unapproved modules | AUTO-VAR | loaded-module approval + approved directory protection |
| V-278388 | II | protect audit information | AUTO | effective file logs inspected; group/other-write asserted |
| V-278389 | II | approved ports/protocols/services | AUTO-VAR | approved listener inventory required |
| V-278390 | II | replay-resistant authentication | EXTERNAL+VAR | auth architecture/evidence required |
| V-278391 | II | CRL validation | AUTO-VAR | applicable only when CRL path selected |
| V-278392 | II | private-key access | AUTO | referenced private keys mode 0600 |
| V-278393 | II | prohibited mobile code/modules | AUTO-VAR | approved module inventory required |
| V-278394 | II | outbound DoS/timeouts | AUTO | <=10s timeout directives |
| V-278395 | II | safe error/version disclosure | AUTO | server_tokens off |
| V-278396 | I | central audit off-load | AUTO-VAR | site syslog endpoint required |
| V-278397 | II | restrict config-file access | AUTO | config directory no other-write |
| V-278398 | II | deny-all permit-by-exception | AUTO-VAR | approved CIDRs required |
| V-278399 | II | SSL reauth <=15m | AUTO | ssl_session_timeout 15m |
| V-278400 | II | PIV credentials | EXTERNAL+VAR | DOD PKI + mTLS/application scope |
| V-278401 | II | expire cached authenticators | AUTO-VAR | N/A unless keyval; org timeout required |
| V-278402 | II | pass security attributes | AUTO-VAR | application-defined proxy headers required |
| V-278403 | II | DOD-approved CAs | HUMAN/EVIDENCE | PKI approval evidence |
| V-278404 | II | DoS protection | AUTO-VAR | global zone + explicitly reviewed server-scope limit; hard-stop otherwise |
| V-278405 | II | FIPS-approved algorithms | AUTO/EXTERNAL | protocol/cipher config + platform validation |
| V-278406 | II | OCSP validation | AUTO-VAR | alternative to CRL; PKI/site values required |
| V-278407 | II | FIPS-validated module | EXTERNAL+VAR | OS/OpenSSL FIPS evidence required |
| V-278408 | II | service account password locked | AUTO | password_lock |
| V-278409 | II | API maintenance separation | HUMAN/ARCH | N/A if API unused; otherwise site network design |
| V-278410 | II | protect token cryptographic keys | AUTO/EVIDENCE | key permissions + cryptographic inspection |
| V-278411 | II | revoke access tokens | APP/EVIDENCE | N/A when tokens unused; IdP/app lifecycle evidence |

## First-pass cautions

V-278384, V-278390, V-278398, V-278400, V-278402, V-278403, V-278406, V-278407, V-278409, and V-278411 can change application access or depend on site architecture. They are intentionally not given invented defaults.

The V1R1 check/fix text also contains examples that require product-version reconciliation before literal automation, particularly OCSP directives and TLS 1.3 cipher handling. These are tracked as high-risk validation items rather than copied blindly.


## Deep static reconciliation — 2026-09-25

The second review compared the executable role against the literal V1R1 checks and current NGINX directive semantics. Changes made before team testing:

- V-278385 now parses every effective custom `log_format` and asserts all ten fields named by the current check.
- V-278387/V-278393 now discover effective `load_module` entries and require every loaded external module to appear in the approved inventory.
- V-278388 now discovers file-based access/error logs and asserts that existing files are not group/other writable.
- V-278404 no longer treats `limit_conn_zone` alone as compliance. It requires an effective `limit_conn`/`limit_req`, or an explicitly reviewed server-scope file for insertion.
- V-278396 remains a CAT I hard stop because the current check requires every existing access/error log directive to use `syslog:server=`; adding a second log destination does not cure a non-syslog directive.
- V-278391 and V-278406 remain mutually alternative CRL/OCSP paths. The V1R1 OCSP fix example is not automated literally because portions conflict with current NGINX directive semantics.
- V-278405/V-278407 remain split between NGINX protocol/cipher configuration and platform cryptographic-module evidence. `ssl_ciphers` is not treated as proof of TLS 1.3 cipher-suite selection or FIPS validation.

No control is considered assessment-verified by this static review.
