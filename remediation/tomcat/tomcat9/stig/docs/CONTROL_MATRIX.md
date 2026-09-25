# Apache Tomcat 9 DISA STIG V3R4 — control/remediation matrix

Baseline: **Apache Tomcat Application Server 9 STIG V3R4 (79 findings)**.

Classification: `AUTO` = deterministic remediation; `AUTO-VAR` = deterministic once an SSP/ISSO/site value is supplied; `EXTERNAL+VAR` = Tomcat/RHEL configuration can be automated but external platform/process evidence remains; `HUMAN/EVIDENCE`/`HUMAN/ARCH`/`PROCESS` = a human or lifecycle decision cannot safely be invented by Ansible.

This repository copy is sourced from the previously developed project matrix. See the role defaults and tasks for implementation boundaries.

## Classification totals

- AUTO: 45
- AUTO-VAR: 25
- EXTERNAL+VAR: 2
- HUMAN/EVIDENCE: 5
- HUMAN/ARCH: 1
- PROCESS: 1

## Stabilization rule

No control is promoted to AUTO merely because a plausible hardening setting exists. Site authorization, RMF applicability, PKI provenance, approved networks/connectors, and production patch approval remain explicit inputs/evidence.
