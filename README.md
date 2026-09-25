# STIG Automation

Automation and validation content for DISA STIGs.

The repository has two primary roots:

- `remediation/` — Ansible lockdown and deterministic Anti-STIG content.
- `scap/` — SCAP/OVAL validation content.

Both use the same technology/benchmark hierarchy so a DISA V-ID can be traced across validation, remediation, intentional failure, and regression testing.

## Tomcat 9 tester quick start

The current Tomcat stabilization target is RHEL 8/9 with Tomcat 9.

From the repository root:

    cp inventories/lab/hosts.example.yml inventories/lab/hosts.yml
    # Edit inventories/lab/hosts.yml for your test host.
    ansible tomcat9 -m ping
    ansible-playbook playbooks/tomcat9_stig.yml --check --diff
    ansible-playbook playbooks/tomcat9_stig.yml

See `TESTING.md` before applying the role and record the exact Git tag/commit with SCAP results.

Current work also includes Apache HTTP Server 2.4 UNIX Server/Site. Anti-STIG implementation is deferred until the corresponding remediation has established a verified compliant baseline.
