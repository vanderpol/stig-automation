# Apache 2.4 UNIX Server STIG remediation

Implementation target: Apache Server 2.4 UNIX Server STIG V3R3.

This role separates deterministic STIG remediation from organization/application decisions. **Do not customize deployments by editing the role.** Put approved site values in inventory `group_vars` or `host_vars`.

Before applying remediation, read:

- `docs/APACHE24_SERVER_USER_GUIDE.md`
- `inventories/lab/group_vars/apache24.yml.example`
- `remediation/apache/apache24/server/stig/docs/CONTROL_MATRIX.md`
- `docs/APACHE24_SERVER_TEST_REPORT.md`

## Expected workflow

1. Define inventory and reusable site/application profile values.
2. Run `playbooks/apache24_server_preflight.yml`.
3. Resolve required site decisions/evidence.
4. Review `ansible-playbook playbooks/apache24_server_stig.yml --check --diff`.
5. Apply to a test system.
6. Validate Apache and the hosted application.
7. Re-run for idempotency.
8. Run the authoritative STIG/SCAP assessment.

A successful Ansible run does not by itself establish STIG compliance. Some controls require application behavior, organizational authorization, architecture, or process evidence.

See the user guide for control classes, profile reuse, evidence handling, secrets, and production-safety expectations.
