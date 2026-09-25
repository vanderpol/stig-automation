# STIG Automation

Automation and validation content for DISA STIGs.

The repository has two primary roots:

- `remediation/` — Ansible lockdown and deterministic Anti-STIG content.
- `scap/` — SCAP/OVAL validation content.

Both use the same technology/benchmark hierarchy so a DISA V-ID can be traced across validation, remediation, intentional failure, and regression testing.

Current work includes Apache HTTP Server 2.4 UNIX Server/Site and Apache Tomcat 9 V3R4. Anti-STIG implementation is deferred until the corresponding remediation has established a verified compliant baseline.
