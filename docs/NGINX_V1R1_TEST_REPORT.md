# F5 NGINX V1R1 initial validation report

Status: **template — not yet lab validated**

## Build
- Git commit/tag:
- Date:
- Tester:
- OS/version:
- NGINX edition (Open Source/Plus):
- NGINX version/package source:
- OpenSSL version/provider:
- Ansible version:
- STIG/assessment content: F5 NGINX V1R1

## Preflight
- Effective main config:
- Runtime user:
- Included config paths:
- Loaded modules:
- Active listeners:
- TLS virtual servers:
- API in use:
- keyval/token features in use:

## Execution
- Preflight result:
- Check/diff reviewed:
- First apply result:
- `nginx -t` result:
- Application functional result:
- Second apply/idempotency result:

## Authoritative assessment
- Pass:
- Fail:
- Not Applicable:
- Not Reviewed:
- Unexpected V-IDs:

## High-risk observations
Record findings for CAT I V-278381/V-278396 and for PKI/FIPS/auth/network controls V-278389-V-278411. Include the literal current-check result and the effective NGINX configuration path inspected.

## Defects/anomalies
For each defect include V-ID, non-secret relevant configuration, Ansible behavior, `nginx -t` result, application impact, authoritative assessment result, and proposed correction. Never include private keys, tokens, or credentials.


## Static-reconciliation gates before team handoff
- [ ] Confirm current effective custom log formats satisfy V-278385.
- [ ] Confirm loaded modules and their real directories satisfy V-278387/V-278393.
- [ ] Confirm every existing file log satisfies V-278388.
- [ ] Confirm every access/error log directive satisfies CAT I V-278396; do not count duplicate syslog logging as a cure for a remaining local-only directive.
- [ ] Confirm V-278404 has an applied limit_conn/limit_req in the intended application scope.
- [ ] Select CRL or OCSP path and document the complementary control as N/A as directed by V1R1.
- [ ] For OCSP, verify installed NGINX edition/version supports the chosen directives and do not create an empty ssl_stapling_file as a cache.
- [ ] Confirm OpenSSL/provider FIPS state independently of NGINX cipher text.
