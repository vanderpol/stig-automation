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

The execution interface for all remediation and Anti-STIG content SHALL follow `docs/LAB_FIRST_EXECUTION_STANDARD.md`. Repository structure may remain modular internally, but that structure SHALL NOT force normal lab testers to edit role files or manually orchestrate preflight steps.


1. Separate SCAP validation from remediation at the repository root.
2. Mirror technology and benchmark hierarchy beneath both roots.
3. Preserve V-ID/STIG-ID/CAT identity through SCAP, lockdown, Anti-STIG, and regression tests.
4. Keep Server and Site benchmarks separate even when controls or directives overlap.
5. Abstract OS/package differences without changing rule identity.
6. Anti-STIGs create deterministic failures for SCAP regression testing; they are not simple inversions of lockdown tasks.
7. Use deterministic current-STIG values as lab defaults when legitimate; do not invent site-specific, architectural, certificate, approval, or organizational facts.
8. Do not commit secrets or production-sensitive inventory data.
