# Benchmark Version Policy

## Current benchmark only

This repository implements the **current benchmark version/release** selected for each role. Historical DISA STIG releases may be useful for change research, but they are not implementation authority and must not be used to fill apparent gaps in a current benchmark.

Current Apache targets:
- Apache Server 2.4 UNIX Server STIG V3R3
- Apache Server 2.4 UNIX Site STIG V2R7

## Why

Controls may be added, removed, rewritten, consolidated, or duplicated between releases and between related Server/Site benchmarks. Carrying historical controls forward can create false findings, duplicate remediation, conflicting configuration, or an inaccurate compliance claim.

Therefore:

1. Build the control ledger from the current release only.
2. Validate each current V-ID against its current check/fix text.
3. Do not reintroduce a V-ID merely because it existed in an older release.
4. Do not assume two similarly worded current controls are duplicates; compare their current check/fix semantics and compliance boundary.
5. When Server and Site overlap, document the overlap and choose the correct implementation/evidence owner rather than applying conflicting fixes twice.
6. When a new benchmark release is adopted, create a deliberate delta review before changing classifications or remediation.
7. Assessment/test results must identify the benchmark version/release used.

Historical material can be cited in change notes, but never as justification for claiming compliance with the current release.
