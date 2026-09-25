# Testing STIG Automation

## Tomcat 9 V3R4 quick start

Supported stabilization targets are RHEL 8 and RHEL 9 running Tomcat 9.

1. Clone the repository and check out the exact tag or test branch supplied for the test cycle.
2. Install Ansible Core 2.14 or newer on the control node.
3. Copy `inventories/lab/hosts.example.yml` to `inventories/lab/hosts.yml` and replace the example host/address/user.
4. If site-specific values are needed, copy `inventories/lab/group_vars/tomcat.yml.example` to `inventories/lab/group_vars/tomcat.yml` and uncomment only approved values. Keep secrets in Ansible Vault or another approved secret store.
5. Verify connectivity:

       ansible tomcat9 -m ping

6. Run preflight/discovery. This does not apply the remediation role:

       ansible-playbook playbooks/tomcat9_preflight.yml

7. Inspect proposed changes:

       ansible-playbook playbooks/tomcat9_stig.yml --check --diff

   Review the diff before proceeding. XML remediation uses an embedded parser and is not executed by Ansible shell in check mode, so the real XML changes will first occur during the apply step.

8. Apply the role:

       ansible-playbook playbooks/tomcat9_stig.yml

9. Run it a second time to check idempotency:

       ansible-playbook playbooks/tomcat9_stig.yml

   A stable target should have no unexpected changes on the second run.

10. Run the corresponding SCAP benchmark and record results using `docs/TOMCAT9_TEST_REPORT.md`.

The role intentionally stops rather than guessing an unknown Tomcat installation layout. If discovery fails, set the explicit Tomcat path variables documented in the role defaults.

## What to report

Please report the Git tag or commit SHA, RHEL major/minor version, Tomcat version/package source, detected Tomcat layout, Ansible version, SCAP content/version, pass/fail/not-applicable counts, unexpected V-IDs, and whether the second Ansible run was idempotent.

## Current pre-release cautions

- Test on disposable/lab systems before production use.
- Back up or snapshot the target before the first apply.
- Review application compatibility before removing the default ROOT application or enforcing production connector/Host settings.
- Site-specific PKI, JMX, LDAP, proxy, connector, and architecture decisions must be supplied explicitly; the role does not invent them.
- Anti-STIG content must not be run on production systems and remains deferred until a compliant baseline is verified.
