# Testing STIG Automation

## Tomcat 9 V3R4 quick start

Supported stabilization targets are RHEL 8 and RHEL 9 running Tomcat 9.

1. Clone the repository and check out the exact tag or test branch supplied for the test cycle.
2. Install Ansible Core 2.14 or newer on the control node.
3. Copy `inventories/lab/hosts.example.yml` to `inventories/lab/hosts.yml` and replace the example host/address/user.
4. Copy only needed values from `inventories/lab/group_vars/tomcat.example.yml` into `inventories/lab/group_vars/tomcat.yml`. Do not commit passwords or other secrets.
5. Verify connectivity:

       ansible tomcat9 -m ping

6. Inspect the proposed changes first:

       ansible-playbook playbooks/tomcat9_stig.yml --check --diff

7. Apply the role:

       ansible-playbook playbooks/tomcat9_stig.yml

8. Run the corresponding SCAP benchmark and record the repository tag/commit, RHEL version, Tomcat version, and SCAP results.

The role intentionally stops rather than guessing an unknown Tomcat installation layout. If discovery fails, set the explicit Tomcat path variables documented in the role defaults.

## Test report minimums

Please report the Git tag or commit SHA, RHEL major/minor version, Tomcat version/package source, detected Tomcat layout, Ansible version, SCAP content/version, pass/fail/not-applicable counts, and the V-IDs for unexpected failures.

Do not test Anti-STIG content on production systems. Anti-STIG implementation remains deferred until the compliant baseline is verified.
