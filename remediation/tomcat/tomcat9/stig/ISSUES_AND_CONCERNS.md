# Apache Tomcat 9 V3R4 — Issues, Concerns, and Validation Notes

Last updated: 2026-09-25  
Status: **pre-team-testing / not assessment-verified**

This is the durable record of known benchmark ambiguities, implementation risks, site-owned decisions, and validation concerns for the Tomcat 9 V3R4 role. Update it whenever testing, authoritative assessment, or a benchmark/vendor change reveals new information.

## Scope and validation boundary

The stabilization target is **RHEL 8 and RHEL 9 with Tomcat 9**. Ubuntu and RHEL 10 are intentionally outside this baseline. All controls remain first-cycle HIGH scrutiny until representative lab, idempotency, functional, and authoritative V3R4 assessment testing is complete.

The September 2026 retrospective review found **14 current V3R4 controls that were missing or only partially represented** by executable remediation/audit logic. Those gaps were closed or converted to explicit evidence/guardrail handling, but this is a strong reason not to equate documentation coverage with tested coverage.

## Benchmark/product-semantic concerns

### V-222971 — proxy/load-balancer mutual authentication

Current Tomcat 9 product semantics use `SSLHostConfig certificateVerification="required"` for mandatory client-certificate verification. The STIG wording can be read as older/different terminology.

The role follows current Tomcat-valid syntax while preserving the STIG requirement intent. Testing must record both Tomcat behavior and authoritative-assessment behavior. Do not rewrite every Connector: only explicitly identified proxied connector/application scope should be changed.

### V-222979 — manager idle timeout

The current check contains inconsistent manager-path wording but explicitly accepts the timeout in `$CATALINA_BASE/conf/web.xml`. The role uses the assessor-accepted global path. Because a global timeout can affect applications beyond Manager, functional testing is required.

### V-222976 — Manager error pages

The benchmark description and check/fix page-number references are not fully consistent. The role follows the current check/fix behavior by replacing the identified Manager error responses with generic content. Validate against the authoritative assessor and installed Manager application version.

## Authentication and Realm blast radius

### V-222962 / V-222965 — LDAP/LDAPS

Management applications require site-supplied directory/JNDIRealm values. LDAP directory structure, credentials, trust, and organizational authentication architecture must not be guessed.

### V-222980 / V-222981 / V-222982 — LockOutRealm

The current assessor path drives the implementation toward Engine-level `server.xml` Realm behavior. An Engine Realm can be inherited by applications other than Manager and can therefore alter authentication across the hosted environment.

The role requires explicit application-impact acknowledgement. Test every hosted application's authentication behavior after this change, not just Manager.

## FIPS and PKI

### V-222968 — FIPS-validated secured connectors

This is a mandatory CAT I requirement. A boolean default must never make it silently disappear.

Tomcat configuration cannot establish that the underlying RHEL/Java cryptographic implementation is FIPS validated. The role therefore requires platform evidence before configuring the Tomcat-side FIPS behavior. Lab testing must record OS FIPS state, Java provider/runtime details, connector configuration, and authoritative assessment results.

### V-222971 and certificate-based authentication

Proxy/load-balancer mTLS depends on PKI material and architecture outside Tomcat. Certificate verification settings are only the Tomcat portion of the control. DoD/organization trust provenance and proxy behavior remain evidence.

## Cluster architecture

### V-222974 — trusted cluster network

The automation cannot determine whether a cluster network is sufficiently trusted/private or whether `EncryptInterceptor` is required. This remains audit/evidence driven. Cluster encryption changes require coordinated testing across all members; never enable them independently on one node without an architecture decision.

## Management access and authorization

### V-222970 — Manager access restrictions

Approved management networks are site-owned. The role can apply supplied `RemoteCIDRValve` or `RemoteAddrValve` semantics but must not invent an allowlist. Test IPv4/IPv6, proxy source-address behavior, and administrative recovery access.

### V-223006 — approved management-role users

Presence of a Tomcat role does not prove that the individual is ISSO-approved. This remains evidence/authorization driven.

### V-223009 — Connector address binding

Every active Connector requires an SSP-approved address mapping. Blindly binding connectors can break local proxies, monitoring, clustering, or application access. Validate every Connector individually.

## Packaging and path concerns

Tomcat packaging/layout differs materially across distributions and installation methods. This role deliberately supports the stabilized RHEL 8/9 layouts and refuses to guess unknown layouts.

Do not extend the role to Ubuntu or RHEL 10 by merely adding an OS condition. Reconcile paths, package ownership, service definitions, XML locations, Java/runtime behavior, and the current benchmark before adding a platform.

## XML mutation concerns

Changes to `server.xml`, `web.xml`, Realm structures, Connectors, and SSLHostConfig are HIGH-risk even when syntactically valid. Testing must include:

- XML/config parse and Tomcat startup;
- preservation of comments/namespace-sensitive content where relevant;
- duplicate-element/idempotency checks;
- authentication and Manager access;
- TLS/mTLS behavior;
- application routing and session behavior;
- a second Ansible run with no unexpected changes.

## Site-owned controls and evidence

Do not invent values for approved networks/connectors, LDAP directory structure, administrative identities, PKI trust, FIPS evidence, cluster trust/encryption, HA, RMF risk acceptance, audit alerting, or production patch approval.

Use required variables, explicit evidence references, hard stops, or documented N/A only where the benchmark genuinely permits N/A.

## Provenance concern

The implementation baseline came from the project-owner-supplied `tomcat9_stig_ansible_rhel8_rhel9_v0.3`. Its upstream ancestry is unresolved. The public Ansible-Lockdown TOMCAT-9-STIG role is reference-only because current V3R4 alignment could not be established.

Do not imply that inherited internal code is current merely because it previously worked.

## Compliance-claim boundary

A successful Ansible run is not evidence that the system is STIG compliant. Until authoritative V3R4 assessment and functional testing are complete, describe this as an **initial validation build / STIG remediation automation**, not an assessment-verified compliant build.

## Anti-STIG

Anti-STIG remains deferred until a representative RHEL 8/9 Tomcat 9 system reaches a verified positive V3R4 baseline.

## Maintenance triggers

Revisit this file when the Tomcat 9 STIG changes, Tomcat product semantics change, a new OS/platform is proposed, an assessor behaves differently from the documented check, or team testing reveals an application-impact/idempotency issue.
