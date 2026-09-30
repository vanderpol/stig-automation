> **LAB / REGRESSION TESTING ONLY — NOT FOR PRODUCTION USE**
>
> This repository exists solely to assist automated regression testing of DISA STIG SCAP content in isolated, disposable test environments. The Ansible content intentionally makes security-relevant configuration changes and may disrupt applications, authentication, networking, logging, TLS, or other services. It is not production hardening guidance and SHALL NOT be used on production, operational, or otherwise valuable systems.

# Apache HTTP Server 2.4 remediation

Ansible remediation and Anti-STIG content for the DISA Apache 2.4 UNIX Server and Site STIGs.


## Known issues and validation concerns

Read the role-specific concern records before testing or deployment:

- [Server STIG issues and concerns](server/stig/ISSUES_AND_CONCERNS.md)
- [Site STIG issues and concerns](site/stig/ISSUES_AND_CONCERNS.md)

These are living records for benchmark ambiguities, implementation risks, application/site boundaries, and unresolved validation items.
