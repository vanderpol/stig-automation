# Repository layout

```
stig-automation/
├── remediation/
│   ├── apache/apache24/
│   │   ├── common/
│   │   ├── server/{stig,anti_stig,tests}/
│   │   └── site/{stig,anti_stig,tests}/
│   └── tomcat/tomcat9/
│       ├── stig/
│       ├── anti_stig/
│       └── tests/
├── scap/
│   ├── apache/apache24/{server,site}/
│   └── tomcat/tomcat9/
├── inventories/
├── playbooks/
├── tests/
└── docs/
```

## Design rules

1. Separate SCAP validation from remediation at the repository root.
2. Mirror technology and benchmark hierarchy beneath both roots.
3. Preserve V-ID/STIG-ID/CAT identity through SCAP, lockdown, Anti-STIG, and regression tests.
4. Keep Server and Site benchmarks separate even when controls or directives overlap.
5. Abstract OS/package differences without changing rule identity.
6. Anti-STIGs create deterministic failures for SCAP regression testing; they are not simple inversions of lockdown tasks.
7. Do not invent defaults for site-specific, architectural, certificate, or organizationally defined values.
8. Do not commit secrets or production-sensitive inventory data.
