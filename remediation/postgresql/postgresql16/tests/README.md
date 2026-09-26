# PostgreSQL 16 remediation tests

Store team validation artifacts under `results/`.

Minimum test sequence:

1. discovery/preflight;
2. check/diff review;
3. apply;
4. approved restart when required;
5. PostgreSQL/application functional testing;
6. second apply/idempotency;
7. authoritative Crunchy Data Postgres 16 V1R3 assessment;
8. V-ID reconciliation.

Use `../docs/TEST_REPORT.md` as the report template.

Never commit credentials, password hashes, private keys, tokens, sensitive connection strings, or production data.
