# STIG Automation

Automation and validation content for DISA STIGs.

Future agent/contributor work must follow `AGENTS.md`. The rationale and reusable Apache/Tomcat lessons are documented in `docs/LOCKDOWN_LESSONS_LEARNED.md`.

The repository has two primary roots:

- `remediation/` — Ansible lockdown and deterministic Anti-STIG content.
- `scap/` — SCAP/OVAL validation content.

Both use the same technology/benchmark hierarchy so a DISA V-ID can be traced across validation, remediation, intentional failure, and regression testing.

## Contributor rule: provenance is mandatory

All new implementation work and substantial modifications must update a provenance/source ledger **as the work is performed**. Do not defer provenance reconstruction until the end of a project.

See `docs/PROVENANCE_POLICY.md` for required fields, classifications, licensing/attribution guidance, and the definition of implementation-complete. Existing work without a contemporaneous ledger must be explicitly identified as retrospective provenance.

## Apache HTTP Server 2.4 tester quick start

Current Apache implementation targets:

- Apache Server 2.4 UNIX Server STIG V3R3
- Apache Server 2.4 UNIX Site STIG V2R7
- RHEL 8/9/10 and Ubuntu 22.04/24.04/26.04

**First-time Apache users should start with `docs/APACHE24_QUICK_START.md`.**

Server and Site are intentionally separate. Apply and validate the Server role first, then apply the Site role for each hosted site/application. Do not edit files under `remediation/apache/apache24/` to customize an environment; put approved site decisions in inventory/group variables.

From the repository root, the basic Server sequence is:

    cp inventories/lab/hosts.apache24.example.yml inventories/lab/hosts.yml
    cp inventories/lab/group_vars/apache24.yml.example inventories/lab/group_vars/apache24.yml
    # Edit both copied files for the real test system and approved values.
    ansible apache24 -m ping
    ansible-playbook playbooks/apache24_server_preflight.yml
    ansible-playbook playbooks/apache24_server_stig.yml --check --diff
    ansible-playbook playbooks/apache24_server_stig.yml

After the Server baseline is tested, create the Site profile and follow the Site steps in `docs/APACHE24_QUICK_START.md`.

A successful Ansible run is not by itself proof of STIG compliance. Some controls require organization/application decisions or evidence. The preflight output identifies site-input and evidence requirements.

Detailed Apache documentation:

- `docs/APACHE24_QUICK_START.md` — start here.
- `docs/APACHE24_SERVER_USER_GUIDE.md` — Server role decisions and responsibilities.
- `docs/APACHE24_SITE_USER_GUIDE.md` — Site/application decisions and responsibilities.
- `docs/APACHE24_FIRST_PASS_STATUS.md` — implementation/testing status.
- `docs/APACHE24_DUPLICATE_REVIEW.md` — current duplicate candidates.
- `docs/APACHE24_PROVENANCE_SUMMARY.md` — source comparison, provenance counts, and risk-based testing priorities.
- `remediation/apache/apache24/server/stig/docs/SOURCE_PROVENANCE.md` — per-V-ID Server provenance ledger.
- `remediation/apache/apache24/site/stig/docs/SOURCE_PROVENANCE.md` — per-V-ID Site provenance ledger.

## Tomcat 9 tester quick start

The current Tomcat stabilization target is RHEL 8/9 with Tomcat 9.

From the repository root:

    cp inventories/lab/hosts.example.yml inventories/lab/hosts.yml
    # Edit inventories/lab/hosts.yml for your test host.
    ansible tomcat9 -m ping
    ansible-playbook playbooks/tomcat9_stig.yml --check --diff
    ansible-playbook playbooks/tomcat9_stig.yml

See `TESTING.md` before applying the role and record the exact Git tag/commit with SCAP results.

**Current Tomcat status:** a retrospective V3R4 provenance/current-check review found 14 previously missing/partial controls. This round added the safe deterministic remediation and explicit site/evidence guardrails needed to represent all 79 current controls. The new logic is not yet lab/assessment verified. See `docs/TOMCAT9_PROVENANCE_REVIEW.md` and `remediation/tomcat/tomcat9/stig/docs/SOURCE_PROVENANCE.md`.

Anti-STIG implementation is deferred until the corresponding remediation has established a verified compliant baseline.

## PostgreSQL 16 development

PostgreSQL remediation is being developed against the current **Crunchy Data Postgres 16 STIG V1R3** only. The legacy Crunchy Data PostgreSQL benchmark is out of scope.

Development/readiness documentation:

- `remediation/postgresql/postgresql16/README.md` — scope and status.
- `remediation/postgresql/postgresql16/stig/docs/BENCHMARK.md` — authoritative benchmark metadata.
- `remediation/postgresql/postgresql16/stig/docs/CONTROL_MATRIX.md` — current V-ID classification/coverage ledger.
- `remediation/postgresql/postgresql16/stig/docs/SOURCE_PROVENANCE.md` — source/provenance ledger.
- `remediation/postgresql/postgresql16/stig/docs/ISSUES_AND_CONCERNS.md` — known risk, assessor, and site-decision concerns.

No PostgreSQL role should be presented for team testing until the complete V1R3 control set has been reconciled to executable remediation/audit/evidence handling.
