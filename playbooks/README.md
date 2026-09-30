# Non-Interactive Lab Quick Start

> **LAB / REGRESSION TESTING ONLY — NOT FOR PRODUCTION USE.** Provided **AS IS**, without warranty. These playbooks intentionally make disruptive security-relevant changes to disposable test systems.

The normal remediation path no longer requires a separate preflight playbook or copied component variable file. Discovery/preflight runs inside the role and deterministic lab defaults are enabled by default.

Create or use any Ansible inventory containing the test host in a generic `stig_targets` group, then run exactly one component playbook:

```bash
ansible-playbook -i /path/to/inventory playbooks/apache24_server_stig.yml
ansible-playbook -i /path/to/inventory playbooks/apache24_site_stig.yml
ansible-playbook -i /path/to/inventory playbooks/tomcat9_stig.yml
ansible-playbook -i /path/to/inventory playbooks/nginx_stig.yml
ansible-playbook -i /path/to/inventory playbooks/postgresql16_stig.yml
```

Legacy component inventory groups remain accepted for compatibility.

## What remains intentionally unresolved

Non-interactive does **not** mean fabricated evidence. A playbook may report controls requiring facts that cannot legitimately be generated locally, such as DoD/organization-approved PKI, external central-log receipt, approved administrative identities, RMF/PPSM decisions, application architecture, or other organizational evidence. Those controls remain visible for assessment reconciliation but do not require editing role source merely to execute the normal lab run.

## Lab defaults

Each role exposes a `*_lab_mode` default enabled for this repository's isolated regression-test mission. Deterministic values can still be overridden with ordinary Ansible inventory/extra variables when a test case needs a specific value.

Separate `*_preflight.yml` playbooks are retained only as diagnostic/troubleshooting entry points. They are not part of the normal workflow.

## Anti-STIG status

Anti-STIG remains gated by the repository rule requiring an authoritative positive baseline first. Placeholder Anti-STIG directories are not silently converted into guessed negative controls. Once a component's lockdown is assessment-verified, its Anti-STIG SHALL use the same one-command, non-interactive lab interface.
