# Lockdown Development Lessons Learned

## Purpose

This document captures reusable lessons from the Apache HTTP Server 2.4 and Apache Tomcat 9 lockdown work. It is intended to prevent future contributors and agents from repeating the same mistakes when implementing a new STIG or porting an existing lockdown to a new release/platform.

The concise mandatory rules live in the repository root `AGENTS.md`. This document explains why those rules exist.

## 1. Start with the current benchmark, not with existing automation

Existing automation is useful, but it is not authoritative.

For every new lockdown:

1. identify the current DISA STIG title/version/release/publication date;
2. enumerate the complete current V-ID set;
3. compare any existing automation against that set;
4. identify removed, added, or materially changed controls before copying implementation logic.

### Tomcat lesson

The public Ansible-Lockdown Tomcat role appeared useful and was labeled maintained, but its documentation still reflected older operating-system assumptions and did not establish alignment to the current V3R4 benchmark. That made it valuable comparison material, but not a safe source of truth.

The same rule applies to our own older content: an internal role can be well engineered and still be incomplete for the current STIG.

## 2. A control matrix is not proof of executable coverage

A spreadsheet or matrix saying every V-ID is classified does not prove that code actually implements or audits every control.

### Tomcat lesson

The Tomcat matrix accounted for all 79 current V3R4 findings, but reconciliation against executable tasks found 14 current controls that were missing or only partially represented. The gap existed because documentation coverage and executable coverage had drifted apart.

### Rule

For every current V-ID, verify all three:

- the matrix has the V-ID;
- executable remediation/audit/evidence handling exists;
- the behavior matches the current check/fix semantics.

## 3. Security-relevant configuration is not necessarily what DISA checks

A configuration change can improve security and still fail the actual STIG assessment.

### Apache V-214256

`ServerTokens` and `ServerSignature` were sensible identity-hardening measures, but the current check also required sanitized/custom error-document behavior. The original remediation was therefore incomplete.

### Apache V-214292

`Options -Indexes` prevents directory listing and is useful defense-in-depth, but the current Site check expects a default document such as `index.html` or equivalent in applicable directories. Treating `-Indexes` as proof of compliance would have been incorrect.

### Rule

Always ask two separate questions:

1. Is this configuration secure/useful?
2. Does this satisfy the literal current DISA check?

Both matter.

## 4. Exact assessor paths matter

STIG checks often inspect a specific configuration file, hierarchy level, or application path. A technically equivalent setting somewhere else may not satisfy the assessment.

### Tomcat Realm lesson

A management-specific Realm in a manager application context can be valid Tomcat configuration, but the current V3R4 LDAP/LockOutRealm checks inspect `server.xml`. The remediation therefore had to account for Engine-level Realm behavior.

That introduced a second problem: an Engine Realm can affect other hosted applications. The correct solution was not to ignore the assessor path or rewrite it silently; it was to require explicit acknowledgement and functional authentication testing.

### Tomcat timeout lesson

The V-222979 current check explicitly accepts a 10-minute timeout in `$CATALINA_BASE/conf/web.xml`, despite inconsistent manager-path wording elsewhere in the check. The remediation therefore uses the path the current assessor explicitly evaluates.

## 5. Product documentation is a second authority for syntax, not for compliance scope

DISA defines the compliance requirement. The product vendor defines valid product syntax and behavior.

### Tomcat V-222971 lesson

Current Tomcat 9 uses `SSLHostConfig certificateVerification="required"` for mandatory client-certificate verification. Current STIG wording contains terminology that can be read as older/incorrect syntax.

Writing an invalid attribute solely to match wording would make the server worse, not compliant.

### Rule

When benchmark wording and product syntax diverge:

- preserve DISA requirement intent;
- use product-valid syntax;
- document the discrepancy;
- capture assessment/scanner behavior during testing.

## 6. Minimize blast radius

Broad remediation can create more risk than the control it is trying to satisfy.

Examples discovered during review:

- proxy mTLS must not rewrite every Tomcat Connector when only one connector is behind a load balancer;
- a manager-network control should not rewrite unrelated application networking;
- a manager session timeout should not unnecessarily modify unrelated application files;
- an authentication Realm change needs explicit acknowledgement because Engine-level inheritance can affect every application.

### Rule

Require explicit target lists or opt-ins when a control can affect unrelated resources.

## 7. Do not invent site architecture

Some controls depend on facts the automation cannot legitimately determine:

- approved networks;
- DoD/organization-approved trust anchors;
- administrative accounts;
- application authentication architecture;
- LDAP directory structure;
- cluster encryption keys;
- RMF risk acceptance;
- HA requirements;
- PPSM approvals;
- vendor-support and patch-process evidence.

Trying to “automate” these by choosing arbitrary defaults produces false compliance.

### Better pattern

Use one of:

- required variable + validation;
- audit output comparing observed state to supplied approved state;
- explicit evidence reference;
- hard stop until the decision exists;
- documented N/A when the benchmark permits it and the environment genuinely qualifies.

## 8. Defaults can create false compliance

A convenient boolean such as `fips_enabled: false` can become dangerous if it allows a mandatory control to disappear.

### Tomcat V-222968 lesson

V-222968 is CAT I. Making Tomcat FIPS remediation optional would allow the role to finish while knowingly leaving a current CAT I finding. The corrected approach hard-stops remediation until the underlying RHEL/Java FIPS platform is prepared and evidence is supplied, then configures Tomcat accordingly.

### Rule

For mandatory requirements, “disabled by default” must not mean “silently ignored.”

## 9. Provenance is also a testing signal

Source tracking is not only licensing documentation.

A newly written control, substantial adaptation, parser, regex, XML mutation, authentication change, or cross-file rewrite has less operational history and therefore deserves more intensive testing.

The repository therefore keeps separate dimensions:

- provenance;
- implementation type;
- test risk;
- validation status.

An inherited control can still be wrong. An original control can be correct. The provenance label tells us where it came from; test risk tells us how aggressively to validate it.

## 10. “Maintained” does not mean “current benchmark”

When evaluating public lockdowns, check:

- benchmark version/release explicitly documented?
- last meaningful implementation update after current STIG publication?
- supported OS/product versions still current?
- V-ID set matches the current benchmark?
- removed V-IDs still present?
- newly introduced V-IDs missing?
- license compatible?
- implementation path matches current product packaging?

If those cannot be established, use the project as a secondary reference only.

## 11. Record anomalies as first-class project knowledge

Do not rely on someone remembering a strange benchmark detail later.

Examples from Tomcat V3R4:

- V-222971 current wording does not cleanly match current Tomcat SSLHostConfig syntax;
- V-222979 contains inconsistent manager-web.xml path language while also accepting global `conf/web.xml`;
- V-222976 description and check/fix page-number references differ.

These belong in documentation and tester instructions because future assessors or automation tools may expose them again.

## 12. Tester feedback should begin when desk review stops adding value

There is a point where more static analysis becomes less useful than real deployment.

A lockdown is ready for **initial validation** when:

- all current V-IDs are represented;
- provenance is documented;
- site-owned decisions are explicit;
- known high-risk controls are identified;
- tester instructions exist;
- no known deterministic implementation gap remains.

It is not yet “compliant” or “validated.”

The next evidence should come from representative systems and authoritative assessments.

## 13. Standard validation sequence

For each platform:

1. record exact Git commit/tag;
2. record OS/product/package source/version;
3. run discovery/preflight;
4. run check/diff where meaningful;
5. review high-risk changes;
6. apply remediation;
7. run product config validation;
8. run application/service functional tests;
9. apply again and check idempotency;
10. run the current authoritative STIG assessment;
11. reconcile every unexpected V-ID;
12. update provenance/test-risk/validation status based on what was learned.

## 14. Anti-STIG belongs after positive-baseline validation

Writing negative tests too early risks encoding our own misunderstanding as a regression test.

The preferred order is:

`STIG remediation -> authoritative PASS baseline -> Anti-STIG one V-ID -> expected FAIL -> reapply remediation -> PASS`

This gives Anti-STIG a trustworthy oracle.

## 15. Recommended structure for future projects

Every substantial lockdown should have:

- benchmark metadata;
- current control matrix;
- role defaults with conservative/site-owned boundaries;
- discovery/preflight;
- deterministic remediation;
- audit/evidence handling;
- provenance ledger;
- tester quick-start;
- test-report template;
- `ISSUES_AND_CONCERNS.md` as a living role-local record of benchmark ambiguities, implementation risks, blast-radius concerns, and unresolved validation items, linked prominently from the role README;
- known anomaly/duplicate notes;
- first-pass/readiness status;
- Anti-STIG only after positive validation.

## Practical starting checklist

Before writing the first task for a new lockdown, answer:

- What is the exact current STIG release and publication date?
- How many current V-IDs exist?
- Which public/internal implementations exist?
- What STIG release do they actually target?
- Were they updated after the current release?
- What licenses apply?
- Which current V-IDs are absent from those implementations?
- Which old V-IDs were removed?
- Which controls require organization/site decisions?
- Which controls can cause broad or destructive changes?
- Which product documentation pages are needed to verify semantics?
- Where will provenance be recorded while implementation is happening?

If those questions are answered first, the implementation phase becomes substantially safer and easier to test.
