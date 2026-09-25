# Apache 2.4 UNIX Site STIG remediation

Implementation target: Apache Server 2.4 UNIX Site STIG V2R7.

Site remediation remains separate from Server remediation because its compliance boundary is a hosted site/application.

Before use, read `docs/APACHE24_SITE_USER_GUIDE.md` and the Site control matrix. Organization-owned PKI material, authorization decisions, application architecture, PPSM approval, and process evidence are not invented by this role.

Recommended order: Server preflight/remediation/assessment, then Site preflight/remediation/assessment.


Before testing or deployment, also read [`ISSUES_AND_CONCERNS.md`](ISSUES_AND_CONCERNS.md). It records known assessor-versus-hardening traps, PKI/application boundaries, and high-risk Site controls.
