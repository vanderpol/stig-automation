# Testing STIG Automation

## Apache HTTP Server 2.4 initial validation

Current targets are Apache Server V3R3 and Site V2R7 on RHEL 8/9/10 and Ubuntu 22.04/24.04/26.04. This is an **initial validation build**, not a compliance-certified release.

Use a representative non-production system and take a snapshot/backup first.

1. Record the exact Git commit/tag, OS version, Apache package/version/source, and Ansible version.
2. Copy `inventories/lab/hosts.apache24.example.yml` to `inventories/lab/hosts.yml`. The example places the same host in both `apache24` and `apache24_site`.
3. Copy `inventories/lab/group_vars/apache24.yml.example` to `apache24.yml`, replace the documentation Listen address with the approved explicit endpoint, and supply only approved site values.
4. Verify Server connectivity and run preflight:

       ansible apache24 -m ping
       ansible-playbook playbooks/apache24_server_preflight.yml

5. Preview changes and save/review the output:

       ansible-playbook playbooks/apache24_server_stig.yml --check --diff

6. Apply Server remediation:

       ansible-playbook playbooks/apache24_server_stig.yml

7. Confirm Apache configtest/application functionality, then run the Server playbook again. Record any unexpected second-run changes as an idempotency defect.
8. Run the current authoritative Server V3R3 assessment and record every unexpected V-ID.
9. After the Server baseline is stable, copy `apache24_site.yml.example` to `apache24_site.yml` and set the real document root and other approved Site inputs.
10. Run Site preflight, preview, and apply:

       ansible apache24_site -m ping
       ansible-playbook playbooks/apache24_site_preflight.yml
       ansible-playbook playbooks/apache24_site_stig.yml --check --diff
       ansible-playbook playbooks/apache24_site_stig.yml

11. Functionally test the hosted application, then run the Site playbook again for idempotency.
12. Run the current authoritative Site V2R7 assessment and reconcile every unexpected result by V-ID.

Use `docs/APACHE24_SERVER_TEST_REPORT.md` for the test record. For Site testing, include the Site assessment counts and application behavior in the same report until a dedicated Site report is added.

### Controls requiring extra scrutiny

All controls still require assessment, but the first cycle should spend additional time on:

- **V-214256** — ErrorDocument handling was corrected during current-check reconciliation.
- **V-214246** — cross-file Listen mutation can affect service availability.
- **V-214269** — every effective SSLCipherSuite must be evaluated.
- **V-214245 / V-214253** — module behavior differs between RHEL and Ubuntu.
- **V-214290** — document-root filesystem must differ from Apache system/config and OS root filesystems.
- **V-214292** — default-document audit must match the site's effective DirectoryIndex behavior.
- **V-214303** — Apache-managed session-cookie remediation is opt-in and requires application/session testing.

Do not enable V-214303 remediation merely to make an assessment green. Enable it only when the site actually uses Apache mod_session and the approved SessionCookieName is known.

### What constitutes a useful defect report

Include the Git commit/tag, OS/version, Apache version/package source, Ansible version, Server or Site role, V-ID, relevant non-secret configuration, exact Ansible failure/change, authoritative assessment result, whether Apache configtest passed, application impact, and whether the second run was idempotent. Never include credentials, private keys, tokens, or other secrets.

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
