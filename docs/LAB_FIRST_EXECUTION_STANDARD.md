# Lab-First Execution Standard

## Intended-use boundary

This standard applies only to isolated, disposable lab systems used for automated regression testing of DISA STIG SCAP content. Repository automation is not intended or approved for production deployment. Streamlining the lab workflow intentionally favors reproducible endpoint state over production change-management safeguards.

## Purpose

This repository primarily builds deterministic compliant and deliberately noncompliant systems in an **isolated test lab** so SCAP/assessment content can be validated against known endpoint states.

The normal tester experience SHALL therefore be simple, repeatable, and trunk-based. Production deployment engineering is not the primary interface.

## Mandatory execution requirements

1. **One-command normal path.** Each supported STIG remediation SHALL provide a repository-root playbook that a tester can run directly after supplying only connection/inventory information that cannot be discovered.
2. **No role-file editing.** A tester SHALL NOT need to edit files under `remediation/` for the normal lab workflow.
3. **Integrated discovery.** Required discovery/preflight SHALL execute automatically as part of the normal remediation playbook. Separate preflight playbooks MAY exist for troubleshooting but SHALL NOT be required for normal use.
4. **Lab defaults.** When the current STIG defines a clear deterministic required value, including requirements phrased as mandatory unless otherwise documented, the role SHOULD use that value as its lab default.
5. **No fabricated organizational facts.** Lab convenience SHALL NOT invent approvals, PKI trust, network authorization, privileged identities, RMF/PPSM decisions, external infrastructure, secrets, or application architecture.
6. **Graceful unresolved controls.** A control that genuinely needs unavailable organization/application input SHALL be reported clearly as unresolved/evidence-required rather than forcing the tester to modify role source.
7. **Validation is automatic.** Where the product provides a configuration validation command, remediation SHALL validate configuration before restart/reload.
8. **Result summary.** A normal run SHOULD make it easy to distinguish remediated controls, audit/evidence controls, N/A/inapplicable controls, unresolved site-owned controls, and execution errors.
9. **Advanced overrides remain available.** Inventory/group variables MAY override lab defaults for targeted scenarios, but normal lab execution SHALL NOT depend on copying and editing large example variable files.
10. **Compliance claims remain assessment-based.** Successful Ansible execution SHALL NOT be represented as proof of STIG compliance; the authoritative assessment remains the validation oracle.
11. **Consistent interface.** Apache HTTP Server, Tomcat, NGINX, PostgreSQL, and future roles SHOULD use the same invocation and result conventions wherever technically possible.
12. **Anti-STIG symmetry.** After a positive baseline is verified, Anti-STIG content SHOULD provide the same streamlined lab experience while preserving bootability, remote administration, package management, Python/Ansible operation, and troubleshooting capability.

## Target tester workflow

The desired positive-baseline workflow is:

```text
fresh lab system
  -> run one STIG playbook
  -> automatic discovery/preflight
  -> deterministic remediation
  -> product configuration validation
  -> clear unresolved/evidence summary
  -> authoritative assessment
  -> expected result: as close to 100% compliant as legitimate automation permits
```

The eventual negative-baseline workflow is:

```text
fresh lab system
  -> run one Anti-STIG playbook
  -> deterministic reversible noncompliance
  -> preserve test-system manageability
  -> authoritative assessment
  -> expected result: as close to 0% compliant as safely practical
```

## Side effects accepted for lab mode

The default lab workflow MAY be more opinionated and disruptive than production automation. It may change listeners, authentication behavior, TLS configuration, modules, default content, permissions, logging, or application behavior when the current STIG requires those changes.

Those effects SHALL still be documented, deterministic, scoped to the target product, and reversible/rebuildable in the disposable lab. Lab mode does not waive the rules against inventing external approvals or knowingly creating invalid product configuration.

## Migration of existing roles

Existing roles SHALL be refactored toward this standard. Until each role is updated, its documentation SHALL identify any legacy manual preflight, copied-variable-file, or source-editing steps that remain.

Refactoring SHALL preserve current benchmark correctness, provenance, known issue records, and advanced variables; simplification is an interface change, not permission to weaken assessment fidelity.
