# RHEL 9.x Anti-STIG Lab Role

> **DANGER — intentionally insecure.** This role exists only to create disposable RHEL 9.x systems that should score poorly against the DISA RHEL 9 STIG. Never run it on production, operational, shared, internet-facing, or irreplaceable systems.

## Purpose

Create a repeatable SCC/STIG assessment fixture while preserving enough system functionality for testing: bootability, networking, SSH/Ansible reachability, Python, DNF/package management, and systemd-journald troubleshooting.

The benchmark authority is **DISA Red Hat Enterprise Linux 9 STIG V2R9 (01 Jul 2026), 445 rules**. SCAP/OVAL/XCCDF benchmark automation was **not used as an implementation source**.

The role requires `rhel9_anti_stig_acknowledge: true` and refuses non-RHEL-9 targets.

## Design

The role uses a broad-first strategy: a relatively small number of deliberately weak configurations produce findings across many related requirements. It does not corrupt files, break package management, alter interface addressing/routes, enable promiscuous mode, weaken SSH host-key file ownership/modes, remove Python, or disable journald.

Start from a fresh RHEL 9.x VM, take a snapshot, run the role, verify SSH still works, then run SCC. Record the SCC result under the repository test-results structure and reconcile unexpected passes/failures to `docs/CONTROL_MATRIX.md`.

## Run

```bash
cp inventories/lab/hosts.rhel9_anti_stig.example.yml inventories/lab/hosts.rhel9_anti_stig.yml
# edit host/address/user/key
ansible -i inventories/lab/hosts.rhel9_anti_stig.yml rhel9_anti_stig -m ping
ansible-playbook -i inventories/lab/hosts.rhel9_anti_stig.yml playbooks/rhel9_anti_stig.yml
```

See `docs/EXCLUSIONS.md`, `docs/SOURCE_PROVENANCE.md`, and `docs/CONTROL_MATRIX.md`.
