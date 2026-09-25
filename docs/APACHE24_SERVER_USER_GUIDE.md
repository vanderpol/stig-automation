# Apache Server 2.4 UNIX Server STIG V3R3 — User Guide

## Purpose

This project separates **STIG implementation logic** from **site decisions**.

The Ansible role implements controls that can be safely and deterministically automated. It does **not** invent organization-specific policy, application architecture, approved accounts, approved network ranges, or other values that the STIG expects the site to define.

A successful Ansible run is therefore not, by itself, a claim that the server is STIG compliant. Final compliance is determined by the applicable STIG checks/SCAP assessment plus required site evidence.

## What end users should edit

Do not edit files under `remediation/apache/apache24/server/stig/` to customize a deployment.

Put reusable organization/application decisions in inventory variables, normally:

`inventories/<environment>/group_vars/apache24.yml`

Use `host_vars` only for genuine host-specific exceptions.

The supplied example is:

`inventories/lab/group_vars/apache24.yml.example`

Copy it to `apache24.yml` and fill in values that apply to the target group.

## Control classes

| Class | Meaning | User expectation |
|---|---|---|
| AUTO | Deterministic server-side remediation | Normally no decision required |
| AUTO-VAR | Automatable after the site supplies an approved value | Set the documented variable before remediation |
| AUDIT-VAR | Ansible can inspect/compare after the site defines the authorization boundary | Supply the approved values; review reported exceptions |
| APP/EVIDENCE | Compliance depends on hosted-application behavior or evidence | Provide/retain evidence; do not expect the server role to manufacture compliance |
| EVIDENCE | Architecture, process, authorization, or operational evidence is required | Maintain the applicable documentation/evidence |

## Recommended workflow

1. Clone or update the repository and select the intended tested version/tag.
2. Create an inventory for the target environment.
3. Copy the Apache group-variable example to the environment's `group_vars/apache24.yml`.
4. Make the required site decisions and record the approved values in that file.
5. Run the preflight playbook. Preflight does not intentionally remediate Apache.
6. Resolve every reported missing site input or evidence requirement that applies.
7. Run the remediation playbook with `--check --diff` and review the proposed changes.
8. Apply remediation to a lab/test server.
9. Confirm `apachectl configtest` succeeds and validate application functionality.
10. Run the playbook a second time and investigate unexpected non-idempotent changes.
11. Run the authoritative STIG/SCAP assessment.
12. Record PASS/FAIL/N/A/manual evidence in the test report.

## Reusing decisions

Group variables are intended to be reusable configuration-as-code. If multiple servers share the same approved architecture, their STIG decisions should be defined once at the appropriate inventory group level and reused across those servers.

Examples include:
- approved Apache Listen IP/port endpoints;
- approved administrative service accounts;
- approved CGI/proxy usage;
- organization-defined blocked/nonsecure networks;
- application categorization and inactivity timeout;
- paths subject to administrative ownership review.

Do not copy a profile between systems unless those systems actually share the same authorization and architecture.

## Required decisions versus defaults

The project intentionally does not provide permissive guesses for values such as approved listeners, administrative accounts, network threat ranges, or application categorization. A missing value should result in a preflight/review condition rather than Ansible silently choosing one.

For example, V-214246 requires explicit site-approved listening endpoints. The role will not substitute `*:443` or `0.0.0.0:443`.

Likewise, V-214247 uses the STIG concept of an administrative service account. The role cannot know which local or enterprise accounts the organization has authorized. It can compare discovered ownership against `apache24_stig_approved_admin_accounts`, but it will not recursively change ownership merely to make the check appear compliant.

## Evidence

Evidence variables are indicators and references for assessment workflow; setting a Boolean or text variable does not create evidence.

Where practical, record a ticket, SSP section, architecture document, SOP, approval record, or other durable reference rather than only setting a value to `true`.

Never store passwords, private keys, tokens, or other secrets in plaintext inventory files. Use Ansible Vault or the organization's approved secret-management system.

## Production safety

Test on representative non-production systems first. Back up configuration and application content or take an appropriate snapshot before the initial remediation run.

Always review `--check --diff`. Apache configuration can be distributed across included files, modules, virtual hosts, and application-specific configuration; a syntactically valid configuration can still cause an application outage.

The role runs an Apache configuration test after remediation, but configtest success is not a substitute for functional testing.

## Compliance boundary

The authoritative benchmark is the DISA Apache Server 2.4 UNIX Server STIG V3R3. The control matrix at `remediation/apache/apache24/server/stig/docs/CONTROL_MATRIX.md` is the implementation ledger.

The role must not promote a control to AUTO simply because a plausible hardening setting exists. Organization-defined authorization, architecture, application behavior, and process requirements remain explicit inputs or evidence.
