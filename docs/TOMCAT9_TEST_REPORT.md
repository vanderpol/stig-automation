# Tomcat 9 test report

Copy this template into an issue or test record for each test system.

## Build

- Git tag/commit:
- Test date:
- Tester:
- Ansible version:
- SCAP content/version:

## Target

- RHEL version:
- Tomcat version:
- Tomcat package/source:
- Detected layout:
- CATALINA_HOME:
- CATALINA_BASE:
- Configuration directory:

## Execution

- Preflight result:
- Check-mode result:
- Apply result:
- Second apply/idempotency result:
- Unexpected Ansible changes/errors:

## SCAP

- Pass:
- Fail:
- Not applicable:
- Not checked/error:
- Unexpected failing V-IDs:

## V3R4 high-scrutiny controls

Record explicit observations for V-222926, V-222962, V-222965, V-222968, V-222970, V-222971, V-222974, V-222976, V-222979, V-222980, V-222981, V-222982, V-223006, and V-223009.

- Management applications installed:
- LDAP/LDAPS authentication functional:
- Existing non-management application authentication impact:
- Manager network restriction functional:
- FIPSMode startup/log result:
- Proxy/load-balancer mTLS result or risk acceptance:
- Cluster network/encryption evidence:
- Manager error pages customized:
- Manager session limit/timeout result:
- LockOutRealm failure/lockout behavior:
- Management-role ISSO approval evidence:
- Every Connector address matches SSP:

## Notes

Include relevant Ansible task output and SCAP evidence. Do not include passwords, private keys, tokens, or other secrets.
