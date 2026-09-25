# STIG Automation

Ansible automation for applying DISA STIG hardening and, after compliant-baseline validation, deterministic Anti-STIG states for SCAP regression testing.

## Repository organization

Content is organized by technology first and benchmark second. Lockdown and Anti-STIG implementations remain siblings so each DISA rule can be traced from compliant state to intentional noncompliant state.

Current work:
- Apache HTTP Server 2.4 UNIX — Server STIG and Site STIG
- Apache Tomcat 9 — V3R4, initially scoped to RHEL 8 and RHEL 9

Anti-STIG content is intentionally deferred until the corresponding lockdown has been tested as compliant.
