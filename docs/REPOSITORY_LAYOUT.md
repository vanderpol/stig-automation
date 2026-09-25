# Repository layout

```
apache/
  apache24/
    common/
    server/
      stig/
      anti_stig/
      tests/
    site/
      stig/
      anti_stig/
      tests/
tomcat/
  tomcat9/
    stig/
    anti_stig/
    tests/
common/
inventories/lab/
playbooks/stig/
playbooks/anti_stig/
docs/
```

## Design rules

1. Technology is the top-level organizational boundary.
2. Separate DISA benchmarks remain separate roles/content sets.
3. OS/package differences are abstracted without changing the STIG rule identity.
4. Rule files retain V-ID/STIG-ID/CAT tags for isolated testing.
5. Anti-STIGs create deterministic failures for SCAP regression testing; they are not simple inversions of the lockdown.
6. Site-specific or architectural requirements use explicit variables or remain evidence/manual controls rather than receiving invented defaults.
