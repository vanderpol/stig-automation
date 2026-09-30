> **LAB / REGRESSION TESTING ONLY — NOT FOR PRODUCTION USE**
>
> This repository exists solely to assist automated regression testing of DISA STIG SCAP content in isolated, disposable test environments. The Ansible content intentionally makes security-relevant configuration changes and may disrupt applications, authentication, networking, logging, TLS, or other services. It is not production hardening guidance and SHALL NOT be used on production, operational, or otherwise valuable systems.

> **NO WARRANTY / USE AT YOUR OWN RISK:** This software and related materials are provided **“AS IS”**, without warranties or conditions of any kind, express or implied, including without limitation warranties of merchantability, fitness for a particular purpose, accuracy, completeness, security, or non-infringement. Use is entirely at your own risk. To the maximum extent permitted by applicable law, the authors and contributors shall not be liable for any claim, damages, data loss, service disruption, security incident, or other liability arising from or related to use of this software. This notice describes intended use and risk; it does not replace or modify the repository's applicable software license.

# F5 NGINX STIG automation

Current benchmark: **F5 NGINX Security Technical Implementation Guide V1R1**, 32 findings (V-278380 through V-278411).

This is an initial-validation implementation. It is not assessment-verified. The role deliberately requires site-owned values for PKI, network policy, logging, authentication, API separation, and token lifecycle controls rather than inventing them.

See `nginx_stig/docs/CONTROL_MATRIX.md`, `SOURCE_PROVENANCE.md`, and the repository `TESTING.md`.


## Known issues and validation concerns

Before using or testing this role, read [`nginx_stig/ISSUES_AND_CONCERNS.md`](nginx_stig/ISSUES_AND_CONCERNS.md). It records known benchmark/vendor discrepancies, CAT I cautions, site-owned controls, application-impact risks, and the remaining validation gates. In particular, review the V-278406 OCSP/stapling discrepancy and the V-278405/V-278407 FIPS validation boundary before treating example STIG configuration as directly automatable.

The role is currently an **initial validation build** and must not be represented as assessment-verified or STIG compliant until the documented lab and authoritative-assessment gates are completed.
