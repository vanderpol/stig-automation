# F5 NGINX V1R1 — Issues, Concerns, and Validation Notes

Last updated: 2026-09-25  
Status: **pre-team-testing / not assessment-verified**

This file is the durable record of known issues, uncertainties, implementation cautions, and items that must be validated before this automation is described as STIG-compliant. It should be updated whenever testing or benchmark/vendor changes reveal a new issue.

## Release boundary

The role targets the **F5 NGINX Security Technical Implementation Guide V1R1**, released 2026-01-07, with 32 findings (V-278380 through V-278411; 2 CAT I and 30 CAT II).

The role has completed a static current-check/vendor-semantics reconciliation. Syntax execution, representative lab testing, idempotency testing, application regression testing, and authoritative assessment remain required.

## Known benchmark/vendor discrepancies

### V-278406 — OCSP / stapling

**High concern. Do not automate the V1R1 fix example literally.**

The V1R1 check/fix text and current NGINX directive semantics are not fully aligned:

- The STIG check example uses an HTTP OCSP responder, while the fix example shows HTTPS.
- Current NGINX documentation states that only `http://` OCSP responder URLs are supported by `ssl_stapling_responder`.
- The STIG fix instructs the administrator to create an empty `ssl_stapling_file` and describes it as a local OCSP cache.
- NGINX documents `ssl_stapling_file` as a file containing a **pre-generated DER OCSP response**, used instead of querying the responder. An empty file is therefore not equivalent to a cache.
- CRL (V-278391) and OCSP (V-278406) are alternative paths in the current checks. The selected path and the complementary N/A determination must be recorded.

Until validated against the installed NGINX edition/version and authoritative assessment behavior, the role must not manufacture the STIG's example OCSP cache.

### V-278405 / V-278407 — FIPS algorithms and validated module

**High concern. NGINX configuration alone cannot prove FIPS compliance.**

- `ssl_protocols TLSv1.2 TLSv1.3` is explicitly configured for the TLS requirement.
- `ssl_ciphers` controls the OpenSSL cipher-list configuration applicable to TLS <=1.2; it must not be treated as proof that TLS 1.3 cipher suites are constrained as intended.
- The installed OpenSSL/provider/module and operating-system cryptographic policy must be independently validated as FIPS-approved/validated.
- Preflight captures `nginx -V` so the linked OpenSSL/build details can be retained with test evidence.

## CAT I concerns

### V-278381 — TLS 1.2 minimum

The role explicitly configures TLS 1.2 and TLS 1.3, but lab testing must confirm that no included server configuration overrides the effective protocol policy.

### V-278396 — central audit off-load

**Hard-stop condition.**

The current check evaluates effective `access_log` and `error_log` directives. Adding an additional syslog destination does not make a remaining local-only log directive compliant. Before declaring this control satisfied:

1. Supply the organization-approved central syslog endpoint.
2. Inventory every effective access/error log directive.
3. Confirm every applicable directive uses `syslog:server=` as required by the current check.
4. Verify actual log delivery to the central service.

The role intentionally does not invent a central logging endpoint.

## Site/application-owned controls

The following controls cannot safely be completed with generic defaults because doing so could break access, authentication, routing, or operational architecture:

- **V-278380** — `worker_connections` is organization/capacity defined.
- **V-278384** — DOD consent banner implementation is application/routing aware.
- **V-278389** — allowed listeners/ports/protocols require SSP-approved inventory.
- **V-278390** — replay resistance depends on the site's authentication architecture.
- **V-278398** — permit-by-exception requires an organization-approved CIDR allowlist.
- **V-278400** — PIV/mTLS requires DOD PKI material and application scope.
- **V-278401** — keyval credential timeout applies only when that mechanism is used and requires an organization-defined timeout.
- **V-278402** — security attributes/proxy headers are application defined.
- **V-278403** — DOD-approved CA/certificate provenance requires evidence.
- **V-278409** — API maintenance separation depends on network/management architecture.
- **V-278411** — token revocation depends on the IdP/application token lifecycle.

These controls must fail safely, require explicit variables/evidence, or remain audit/evidence items rather than receiving guessed values.

## Implementation-specific concerns

### V-278385 — audit fields

The role now parses effective custom `log_format` directives and asserts the ten fields named by the current V1R1 check. Lab testing must include configurations with multiline/complex log formats to confirm the parser handles real deployments correctly.

### V-278387 / V-278393 — external modules

Effective `load_module` paths are discovered and compared with an explicit approved-module inventory. Risks still requiring validation:

- relative module paths and package-specific module directories;
- modules compiled statically rather than loaded with `load_module`;
- organization approval is evidence-driven and cannot be inferred from presence on disk;
- changing ownership/permissions on package-managed module directories must not interfere with package maintenance.

### V-278388 — audit log permissions

The role discovers file-based access/error logs and checks group/other write access. Validate log rotation behavior, newly created file modes, package-specific log locations, and syslog-only deployments.

### V-278392 / V-278410 — private/token cryptographic keys

Referenced TLS private keys are protected with restrictive file permissions, but permissions alone do not prove key strength, generation method, approved storage, or the lifecycle of keys used for application access tokens. Cryptographic inspection/evidence remains necessary.

### V-278394 — timeouts

The global timeout values are deterministic and match the current check intent, but application regression testing is required. Long uploads, slow clients, streaming behavior, and proxied applications can be affected by aggressive timeouts.

### V-278399 — TLS session timeout

The role sets the current STIG value globally. Verify that server-specific configuration does not override it and that the value does not create unexpected application/session behavior.

### V-278404 — DoS protection

A `limit_conn_zone` definition by itself does **not** enforce a connection limit. The role therefore requires an effective `limit_conn`/`limit_req`, or an explicitly reviewed server configuration file where `limit_conn` may be inserted.

Do not blindly apply the same per-client limit to every virtual server. Reverse proxies, NAT, health checks, APIs, websocket/long-lived connections, and high-concurrency applications can require different values.

## Configuration-layout concerns

The role currently assumes a conventional main configuration at `/etc/nginx/nginx.conf` unless overridden and verifies that a managed `conf.d/*.conf` drop-in would actually be included before writing it.

Testing must cover the supported package/layout combinations. Do not assume that NGINX Open Source, NGINX Plus, vendor packages, distribution packages, containers, and appliance-like deployments share identical include paths, module paths, service names, or OpenSSL builds.

## Automation behavior that must be tested

Before team handoff/release, validate:

- YAML/Ansible syntax and module argument validity.
- Preflight discovery against representative NGINX configurations.
- `--check --diff` behavior.
- First application followed by successful `nginx -t`.
- Handler ordering and reload behavior.
- Second-run idempotency.
- No unexpected ownership/mode changes to package-managed paths.
- Application/TLS/authentication/logging functionality after remediation.
- Current authoritative F5 NGINX V1R1 assessment with every unexpected V-ID reconciled.

## Compliance-claim boundary

A successful Ansible run is **not** evidence that the host is STIG compliant. The role deliberately separates deterministic remediation from organization-defined values, architecture, external PKI/FIPS state, and human evidence.

Until the authoritative assessment cycle is completed, documentation and release notes should use language such as **initial validation build** or **STIG remediation automation**, not **STIG-compliant build**.

## Anti-STIG

Anti-STIG development remains intentionally deferred. It should not begin until a representative system reaches a verified positive baseline and the forward remediation behavior is understood well enough to produce safe, reversible negative-test cases.

## Maintenance

Re-run the benchmark/current-vendor reconciliation whenever:

- DISA/F5 publishes a new NGINX STIG version or release;
- NGINX changes relevant directive semantics;
- supported operating systems or NGINX editions are expanded;
- authoritative assessment behavior differs from the documented check;
- team testing finds an application-impact or idempotency issue.

Do not silently resolve a benchmark/vendor conflict in code. Record the discrepancy here, cite the affected V-ID, and document the chosen behavior and validation evidence.


## Structural validation round — 2026-09-25

The pre-team-testing static structural pass corrected several implementation risks:

- V-278383 privileged-group removal is now membership-conditioned and no longer suppresses command failures.
- V-278380 now fails safely if no existing `worker_connections` directive is discoverable rather than silently making no change.
- V-278404 refuses files with an ambiguous number of `server {}` blocks before inserting a limit.
- Handler flow now gates reload through `nginx -t`.
- Handlers are flushed and effective configuration is re-dumped before post-remediation audit, preventing stale pre-remediation facts from satisfying/failing checks.
- V-278404 audit now requires the applied limit to appear in refreshed effective configuration.
- V-278390 and V-278402 now have explicit applicability inputs rather than unconditionally requiring evidence for deployments where the feature is not used.
- V-278396 now checks effective log directives for syslog-backed logging in addition to requiring the site-owned endpoint.

This was a **static structural review**, not execution of `ansible-playbook --syntax-check`. The repository was reviewed through source control; no representative NGINX host or Ansible runtime was available in this review environment. Actual syntax/module execution remains the first tester gate.

### Remaining first-test concerns

- Confirm the handler notification chain validates before the service reload on the team's installed Ansible version.
- Confirm `nginx -qT` output behavior and parser assumptions on each supported package/edition.
- Confirm the managed `conf.d/*.conf` include is in a legal `http {}` context; `nginx -t` is the final guard against an invalid context.
- V-278404 deliberately rejects ambiguous multi-server target files; more complex layouts require a more precise site-owned integration method.
- V-278396's effective-config regex must be compared with the authoritative assessment and real logging layouts, including inherited/default logging behavior.
- Configuration directory/file permission scope for V-278386/V-278397 and exact log permission semantics for V-278388 remain important authoritative-assessment reconciliation points.
