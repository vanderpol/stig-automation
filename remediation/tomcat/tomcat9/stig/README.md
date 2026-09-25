# Tomcat 9 V3R4 STIG remediation

Current implementation scope: **RHEL 8 and RHEL 9 with Tomcat 9**.

## Current repository status

The role skeleton and the first deterministic controls have been carried into this repository:

- authoritative path discovery with fail-safe behavior rather than guessed paths
- conf/log/temp/work permissions and ownership
- Tomcat service account nologin
- systemd UMask 0027
- audit watches for bin/conf/lib
- explicit site/SSP variables in defaults
- V-ID tags on implemented controls

The complete prior control/remediation matrix is under `docs/CONTROL_MATRIX.md`.

## Important carry-over note

The prior project produced a v0.3 role archive, but the complete archive is not currently available through the retained project files. Only the control matrix and automated-rule list are retrievable. Therefore this repository is **not** being populated with guessed copies of unretrievable files. Remaining rule implementations will be rebuilt/verified against the V3R4 matrix and official STIG intent before being marked implemented.

Anti-STIG remains deferred until a compliant baseline is demonstrated.
