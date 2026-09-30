# Tomcat 9 V3R4 STIG remediation

Current implementation scope: **RHEL 8 and RHEL 9 with Tomcat 9**.

This directory is now reconciled from the original `tomcat9_stig_ansible_rhel8_rhel9_v0.3` project supplied by the project owner. The v0.3 files, rather than the earlier reconstructed skeleton, are the implementation baseline.

## Role flow

- `tasks/discovery.yml` — selects the RHEL RPM or explicit Apache-standard layout and refuses to guess unknown layouts.
- `tasks/remediation.yml` — deterministic and variable-driven remediation.
- `tasks/xml_remediation.yml` — idempotent server.xml/web.xml changes.
- `tasks/audit.yml` — human/evidence/process checks that must not be silently converted into invented technical settings.
- `defaults/main.yml` — site/SSP/ISSO inputs and safe defaults.

## Scope

RHEL 8 and RHEL 9 are the stabilization targets. Ubuntu and RHEL 10 remain outside this Tomcat 9 baseline.

Anti-STIG remains deferred until this role produces a verified compliant SCAP baseline.


## Known issues and validation concerns

Read [`ISSUES_AND_CONCERNS.md`](ISSUES_AND_CONCERNS.md) before testing or deployment. It records benchmark ambiguities, Realm/authentication blast-radius concerns, FIPS/PKI boundaries, platform/layout limitations, and remaining validation gates.
