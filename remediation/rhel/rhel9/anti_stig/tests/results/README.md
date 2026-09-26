# RHEL 9 Anti-STIG Test Results

Store sanitized tester results for the RHEL 9.x Anti-STIG here.

Each result should identify:
- exact repository commit SHA;
- RHEL 9.x minor release and image/source;
- Ansible Core version;
- SCC version;
- DISA RHEL 9 benchmark version/release used by the tester;
- PASS/FAIL/Not Applicable/Not Reviewed counts;
- unexpected PASS IDs;
- unexpected errors or system-function impact;
- confirmation that SSH, networking, Python, DNF, and journald remained usable.

Do not commit credentials, private keys, host-identifying sensitive data, raw SCAP implementation content, or scanner rule logic. SCC output may be attached as validation evidence when appropriate, but it must not be used as an implementation source for the Anti-STIG.
