# Team STIG test results

Commit team validation evidence here so results can be reviewed against the exact remediation version that produced them.

## Directory layout

- `nginx/f5-nginx-v1r1/`
- `tomcat/tomcat9-v3r4/`
- `apache/apache24-server-v3r3/`
- `apache/apache24-site-v2r7/`

Create one subdirectory per test run:

`YYYY-MM-DD_<tester-or-team>_<platform>_<short-commit>/`

Copy the component's `SUBMISSION_TEMPLATE.md` into that directory as `RESULTS.md`, complete it, and add sanitized supporting evidence when useful.

## Required traceability

Every submission must record the exact Git commit tested, benchmark/release, target OS/product/package versions, Ansible version, execution results, idempotency result, authoritative assessment counts and unexpected V-IDs.

## Safe evidence

Do **not** commit passwords, private keys, tokens, cookies/session identifiers, LDAP bind credentials, internal secrets, sensitive host inventories, or unredacted configuration containing credentials. Prefer minimal sanitized excerpts needed to explain a finding.

Useful sanitized artifacts can include Ansible output, product configuration-test output, package/build information, authoritative assessment summaries/results, and relevant non-secret effective-configuration excerpts.

## Review status

A committed result is test evidence, not automatically proof of compliance. Findings should be reconciled into the control matrix, provenance/validation status, and `ISSUES_AND_CONCERNS.md` as appropriate.
