# Apache 2.4 Current-Benchmark Duplicate Review

Scope is deliberately limited to the current benchmarks:
- Server V3R3
- Site V2R7

## Candidate duplicate identified

### Server V-214244 ↔ Site V-214282

Server V-214244: Apache must allow mappings to unused and vulnerable scripts to be removed.

Site V-214282: Apache must allow mappings to unused and vulnerable scripts to be removed.

Status: **candidate cross-benchmark duplicate — report to DISA for review.**

These current findings have the same requirement title and address the same script-mapping capability. Keep both V-IDs in assessment results until DISA changes the benchmarks; do not silently drop either finding.

Automation ownership: implement the underlying Apache capability once in shared/server-safe logic where practical, then map/report both V-IDs without applying conflicting duplicate remediation.

## Review method

For every remaining rule:
1. Compare current title, description, check, fix, CCI/SRG mapping, and scope.
2. Flag same-benchmark and Server↔Site candidates separately.
3. Do not classify two controls as duplicates solely from similar titles.
4. Keep both current V-IDs operational until DISA formally changes the benchmark.
