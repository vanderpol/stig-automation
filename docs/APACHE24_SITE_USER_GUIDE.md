# Apache Server 2.4 UNIX Site STIG V2R7 — User Guide

## Design

The Site STIG is intentionally separate from the Server STIG. The Server role hardens the Apache instance. The Site role evaluates/remediates requirements belonging to a particular hosted site/application.

Run the Server STIG first. A server hosting multiple applications may require one Server assessment and multiple Site assessments/profiles.

## What this automation will not decide for you

The role does not download, create, select, or approve DoD PKI trust anchors, client CA bundles, server certificates, or private keys. The end user/organization must obtain and maintain approved PKI material through its authorized process and document the approval boundary.

The role also does not invent:
- application authentication/user-management architecture;
- RFC 5280/revocation implementation evidence;
- authorized private-key administrators/PKI sponsors;
- PPSM approvals or nonstandard ports;
- application operational tuning/capacity values;
- disaster-recovery procedures;
- organization/application network restrictions.

Where possible, Ansible will inspect supplied paths/settings and report measurable facts. Authorization remains a site responsibility.

## PKI responsibilities

When PKI applies, the user must supply the configured CA bundle/trust-store path and evidence that the CAs accepted for client authentication are DoD PKI or otherwise DoD-approved. The role must not treat possession of a CA file as proof that every CA in it is approved.

The user must also configure and document RFC 5280-compliant certification-path validation, including the applicable revocation-validation mechanism.

Private keys must be protected so only authenticated system administrators or the designated PKI Sponsor have access. Supply the private-key path and the site's approved-account boundary; the role can inspect ownership/mode but cannot decide who the organization has authorized.

Never commit private keys, certificate passwords, tokens, or other secrets to this repository.

## Reusable site profiles

Put site decisions in inventory variables, not in the role. A useful model is one inventory group/profile per hosted application or common application class.

Do not reuse a Site profile merely because two applications run on the same Apache instance. Reuse it only when the applications share the same approved security architecture and values.

## Workflow

1. Complete and validate the Apache Server V3R3 baseline.
2. Create the hosted site's inventory group/profile.
3. Run `playbooks/apache24_site_preflight.yml`.
4. Resolve required organization/application decisions and evidence.
5. Review Site remediation with `--check --diff`.
6. Apply to a representative test environment.
7. Functionally test the application, authentication, TLS/client-certificate behavior, and recovery/operations as applicable.
8. Run the authoritative Site V2R7 assessment.
9. Record manual/evidence findings alongside automated results.

A successful Ansible run is not a complete Site STIG assessment.
