# Intentional Exclusions and Preservation Boundary

The goal is a very low assessment score, **not** a dead VM. Every control deliberately left compliant or not forcibly inverted for safety is recorded here. Other controls may remain EXPECTED/ASSESS because they are environmental, manual, naturally noncompliant on a fresh install, or not yet worth forcing before the first SCC result.

| STIG ID / area | Decision | Reason |
|---|---|---|
| RHEL-09-211010 | Excluded | Making the OS vendor-unsupported would require changing/downgrading the platform. |
| RHEL-09-211015 | Excluded from forced failure | Do not deliberately uninstall security errata or downgrade packages. |
| RHEL-09-211040 | Excluded | systemd-journald stays enabled so failed test systems remain diagnosable. |
| RHEL-09-211045, RHEL-09-211050 | Excluded | Do not intentionally enable Ctrl-Alt-Delete reboot behavior; an accidental console key sequence should not destroy a test run. |
| RHEL-09-212010 through RHEL-09-212045 | Excluded from forced failure | Avoid bootloader credentials, ownership, and kernel-command-line changes that could make the VM unbootable or require a reboot merely to manufacture findings. |
| RHEL-09-214010, RHEL-09-214030 | Excluded from destructive inversion | Do not install unsigned/corrupt packages or modify RPM-owned files merely to create package-integrity findings. |
| RHEL-09-215010 | Excluded | Preserve subscription-manager/RHSM integration because it can be required for RHEL repository/package access. |
| RHEL-09-215100 | Excluded | Preserve the crypto-policies package; the role weakens the active policy instead of removing platform crypto-policy machinery. |
| RHEL-09-231xxx filesystem/partition controls | Not forcibly inverted | No repartitioning, destructive remounting, filesystem damage, or removal of at-rest encryption. Natural/default findings remain useful. |
| RHEL-09-251040 and interface-address/route controls | Excluded | Do not place interfaces into promiscuous mode or delete/alter addresses, routes, nameservers, or NetworkManager connection profiles. |
| RHEL-09-255010, RHEL-09-255015, RHEL-09-255020 | Excluded | Preserve OpenSSH server/client packages and basic SSH transport. |
| RHEL-09-255035 | Excluded | Public-key authentication remains enabled so key-based Ansible access continues to work. |
| RHEL-09-255050 | Excluded | Keep UsePAM enabled to avoid breaking SSH session/account behavior. |
| RHEL-09-255105, RHEL-09-255110, RHEL-09-255115 | Excluded | Preserve ownership and safe parsing of SSH configuration files. |
| RHEL-09-255120 | Excluded | Preserve SSH private-host-key modes; OpenSSH can reject unsafe private keys and strand the host. |
| RHEL-09-411030, RHEL-09-411110 | Excluded | Do not create duplicate UID/GID identities merely to create findings. |
| RHEL-09-411095 | Not forcibly inverted | Do not create an arbitrary unauthorized login account; authorization is site/evidence dependent. |
| RHEL-09-432010 | Excluded | Preserve sudo for Ansible privilege escalation and recovery. |
| RHEL-09-611155 | Excluded | Do not create or unlock an account with a blank/null password. PermitEmptyPasswords=yes is sufficient to test the SSH policy finding without creating a usable blank-password account. |
| RHEL-09-611195, RHEL-09-611200 | Excluded | Do not weaken emergency/single-user boot authentication because this crosses the boot/recovery boundary. |
| RHEL-09-653085 and audit daemon runtime availability | Excluded | Preserve root ownership of the audit log directory and do not intentionally stop a running audit daemon; configuration/rule findings are created without making the host undiagnosable. |
| RHEL-09-653105 | Excluded from forced failure | Do not intentionally disable current audit record writes. |
| RHEL-09-653120 | Excluded | Avoid boot-command-line/reboot changes solely to lower audit backlog settings. |
| Services whose only inverse requires exposing a new listener | Generally excluded | Do not install/start FTP, TFTP, telnet, NFS, or similar network services merely to manufacture a finding. Package-absence findings may therefore remain pass/N/A on a fresh image. |
| Python, DNF/RPM, systemd | Preserved | Required to continue automation and diagnosis. |

## SSH guard

Weak SSH policy is allowed, but every change is followed by sshd -t before restart and again in postflight. The role intentionally keeps public-key authentication and PAM enabled.

## Audit-rule handling

Existing /etc/audit/rules.d/*.rules files are renamed to *.rules.anti-stig-disabled rather than deleted. The running audit daemon is not forcibly reloaded or stopped. This creates a deliberately weak configured state while preserving evidence and reducing the chance of losing the active management session.

When tester feedback identifies an unexpected PASS, add a targeted inverse only if it remains inside this preservation boundary. Otherwise add the specific STIG ID here.
