# Source and Provenance Ledger

## Source hierarchy

1. **Primary authority:** DISA Red Hat Enterprise Linux 9 STIG V2R9, released 01 Jul 2026.
2. **Preferred official implementation reference identified:** DISA supplemental `U_RHEL_9_V2R9_STIG_Ansible.zip` (official Cyber Exchange catalog entry, uploaded 10 Jul 2026). The archive itself was not retrievable through the connected tooling during this development pass, so no local task is claimed as inherited from or verified against its code.
3. **Implementation-mechanics reference actually inspected:** ansible-lockdown/RHEL9-STIG public role, devel commit `f6601bf8deb70302954863c9c90272b719b993ed`, MIT license. Its public branch states V2R8, so it is not authoritative for V2R9 requirements. It was used to identify product paths, package names, control groupings, and ordinary Ansible techniques; current V2R9 release/delta information governs inclusion.
4. **V2R9 delta cross-check:** public V2R9 change summaries were used only to verify that RHEL-09-255130 was removed and no rule was added.

## Implementation provenance

| Area | Provenance | Material used | Local difference | Risk |
|---|---|---|---|---|
| Safety/preflight | ORIGINAL | Repository AGENTS/lessons | Explicit lab acknowledgement and RHEL 9 assertion | HIGH |
| package/service inversions | COMMON/ADAPTED | Standard DNF/systemd remediation patterns | Logic inverted to create findings while preserving journald/networking | HIGH |
| sysctl inversions | COMMON/ADAPTED | Standard sysctl remediation patterns | Values intentionally set opposite secure posture | HIGH |
| SELinux/crypto | COMMON | Vendor-supported commands/modules | Permissive/DEFAULT chosen rather than disabling platform mechanisms destructively | HIGH |
| SSH | ORIGINAL/COMMON | OpenSSH directives named by STIG remediation sources | Weak values, but no weak host-key permissions/ciphers; `sshd -t` gate before restart | HIGH |
| password/faillock | COMMON/ADAPTED | Standard pwquality/faillock mechanisms | Values intentionally weaken policy | HIGH |
| file permissions | ORIGINAL/COMMON | Literal permission requirements | Selected noncritical files made permissive; SSH key/config safety boundary retained | HIGH |
| control enumeration | ADAPTED | ansible-lockdown V2R8 446-rule variable set | Removed RHEL-09-255130 per V2R9 delta -> 445 | HIGH |

## SCAP contamination control

No SCC results, SCAP benchmark XML, OVAL definitions, SCAP Security Guide rule logic, or scanner-specific test expressions were used to choose Anti-STIG values. SCC output is **validation evidence only after implementation**, never a design source for how a rule is detected.


## Validation state

- Repository Ansible syntax workflow: passing after the collection-free rewrite and YAML-regex correction.
- Explicit anti-control mappings: 191 of 445 current V2R9 rule IDs before applicability/N/A is known.
- Runtime RHEL 9.x deployment: not yet performed through this environment; team lab execution is the next source of evidence.
- SCC/SCAP results: intentionally not consulted during implementation. First SCC results are validation evidence only.
