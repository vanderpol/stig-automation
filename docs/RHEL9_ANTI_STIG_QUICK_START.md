# RHEL 9.x Anti-STIG Quick Start

This is an intentionally insecure **test fixture** for isolated SCC/STIG labs.

1. Provision a fresh RHEL 9.x VM and confirm SSH/Ansible access.
2. Take a hypervisor snapshot.
3. Copy `inventories/lab/hosts.rhel9_anti_stig.example.yml` and enter the real test host.
4. Verify `ansible ... -m ping`.
5. Run `ansible-playbook ... playbooks/rhel9_anti_stig.yml`.
6. Immediately verify a second SSH login, `dnf --version`, `python3 --version`, `ip addr`, `ip route`, and `journalctl -b -n 50`.
7. Run the authoritative SCC assessment using the lab's independently supplied SCAP content.
8. Record exact RHEL release, repository commit SHA, SCC version, benchmark V2R9, pass/fail/not-applicable counts, and any unexpected PASS IDs.
9. Revert the VM snapshot when finished.

Do **not** tune the role by reading SCAP/OVAL logic. Reconcile unexpected results against the current DISA manual STIG and non-SCAP implementation sources only.

Known preservation exclusions are maintained in `remediation/rhel/rhel9/anti_stig/docs/EXCLUSIONS.md`.
