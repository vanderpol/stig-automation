# Apache HTTP Server 2.4 initial-validation test report

Use one copy per target/application combination. Do not include secrets.

## Build
- Git commit/tag:
- Test date:
- Tester:
- Ansible version:
- Assessment/SCAP tool and content version:

## Target
- Distribution and exact version:
- Kernel/architecture:
- Apache version:
- Apache package source/repository:
- apachectl path:
- HTTPD_ROOT:
- SERVER_CONFIG_FILE:
- Document root:
- Approved Listen endpoints:
- Reverse proxy/load balancer present (yes/no/details):
- Site uses Apache mod_session (yes/no):
- Site profile/hostname:

## Server V3R3 execution
- Connectivity:
- Preflight:
- Check/diff reviewed:
- First apply:
- Apache configtest:
- Application functional test:
- Second apply/idempotency:
- Unexpected changes/errors:

## Server V3R3 assessment
- Pass:
- Fail:
- Not applicable:
- Not checked/error/manual:
- Unexpected V-IDs and observed state:

## Site V2R7 execution
- Preflight:
- Check/diff reviewed:
- First apply:
- Apache configtest:
- Application functional test (TLS/auth/cookies/sessions/URLs/redirects):
- Second apply/idempotency:
- Unexpected changes/errors:

## Site V2R7 assessment
- Pass:
- Fail:
- Not applicable:
- Not checked/error/manual:
- Unexpected V-IDs and observed state:

## High-scrutiny observations
Record explicit results for V-214246, V-214256, V-214269, V-214290, V-214292, V-214303, and any distro-specific V-214245/V-214253 behavior.

- V-ID:
  - Expected:
  - Observed:
  - Ansible result:
  - Assessment result:
  - Application/service impact:
  - Notes:

## Evidence/manual controls
List evidence-required controls that remain unresolved. Supplying an inventory evidence reference does not itself establish compliance.

## Notes
Do not include passwords, private keys, tokens, session secrets, or other sensitive material.
