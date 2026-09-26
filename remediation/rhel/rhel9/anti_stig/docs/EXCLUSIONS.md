# Intentional Exclusions and Preservation Boundary

The goal is a very low assessment score, **not** a dead VM. Every intentional exclusion must be recorded here.

| Area / representative STIG ID | Decision | Reason |
|---|---|---|
| RHEL-09-211010 | Excluded | Making the OS vendor-unsupported would require changing/downgrading the platform. |
| RHEL-09-211015 | Excluded from forced failure | Do not deliberately uninstall security updates or downgrade packages. A fresh image may already be behind current errata. |
| RHEL-09-211040 | Excluded | systemd-journald stays enabled so failed test systems remain diagnosable. |
| RHEL-09-212010/212015/212020/212025 and boot-chain controls | Excluded from forced failure | Avoid bootloader/boot-chain changes that could make snapshot recovery harder or prevent boot. |
| RHEL-09-214030 | Excluded | Do not corrupt RPM-owned files merely to create integrity findings. |
| Filesystem partition/mount-option controls (many RHEL-09-231xxx) | Not forcibly inverted | No repartitioning, destructive remounting, or filesystem damage. Natural/default findings remain useful. |
| RHEL-09-251040 | Excluded | Do not place interfaces into promiscuous mode or otherwise alter interface behavior. |
| Network addressing/routes/DNS required for lab access | Preserved | No task may delete addresses, routes, nameservers, or NetworkManager connection profiles. |
| SSH host/private key ownership and modes, including RHEL-09-255120 boundary | Preserved | OpenSSH can refuse unsafe key files and strand the Ansible session. |
| SSH daemon syntax | Guarded | Weak policy is allowed, but `sshd -t` must pass before restart. |
| Connecting account/root credentials | Preserved | Do not blank, corrupt, expire, or lock the account used for Ansible/SSH. |
| Python, sudo, DNF/RPM, systemd | Preserved | Required to continue automation and diagnosis. |
| audit immutable/early-boot controls requiring risky reboot semantics | Not forcibly inverted | Prefer runtime/config findings that do not threaten bootability. |
| Services whose only inverse requires exposing a new network listener | Generally excluded | Do not open unnecessary network services solely to manufacture a finding. |

When tester feedback identifies an unexpected PASS, add a targeted inverse only if it remains inside this preservation boundary. Otherwise record the rule as intentionally excluded.
