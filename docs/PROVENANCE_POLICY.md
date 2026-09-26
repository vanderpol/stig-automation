# Provenance and Source Ledger Policy

## Mandatory rule for all future work

Every remediation implementation, audit/evidence control, Anti-STIG test, benchmark port, or substantial modification in this repository must maintain a provenance/source ledger **while the work is being created**.

Provenance is not an optional after-the-fact documentation task. A work item is not considered implementation-complete until its ledger is updated.

This rule applies to new work and to changes of existing content, regardless of whether the work is performed in ChatGPT, Codex, an IDE, by hand, or by another contributor.

## Why

STIG automation often resembles existing public implementations because the benchmark prescribes the same underlying configuration. Similarity alone does not prove derivation. Conversely, adapted or inherited implementation should not lose its history.

Recording provenance at implementation time is also a **test-risk control**, not merely attribution. Newly created or substantially modified implementations have less inherited operational history and should receive greater scrutiny during the first validation cycles.

Recording provenance at implementation time lets maintainers:
- distinguish work derived directly from current DISA requirements from work influenced by another project;
- identify inherited/adapted code and applicable licenses/attribution;
- understand what was changed and why;
- evaluate upstream fixes and future benchmark changes;
- identify controls that appear genuinely new for the current benchmark;
- avoid reconstructing development history after the fact;
- identify which controls need the most intensive testing because their implementation is new, substantially modified, platform-specific, or otherwise less proven.

## Required ledger fields

Each current V-ID/control must record, as applicable:

| Field | Requirement |
|---|---|
| V-ID/control | Current benchmark identifier |
| Benchmark | Version/release used as implementation authority |
| Provenance | ORIGINAL, COMMON, ADAPTED, INHERITED, or NEW-CURRENT |
| Implementation type | REMEDIATION, AUDIT, EVIDENCE, APP/EVIDENCE, or mixed form such as REMEDIATION/AUDIT |
| Primary authority | Current DISA STIG/check/fix source |
| Reference source(s) | Public repository/project/document consulted |
| Source version | Tag, release, or commit when available |
| Source location | Role/task/file/control identifier or URL/reference |
| License | License of materially used source |
| Material used | What concept/code/approach informed the implementation |
| Local changes | What this repository changed from the source |
| Reason | Why the local implementation differs |
| Contributor/date | Useful development-history context |
| Test-risk | HIGH, MEDIUM, or BASELINE scrutiny |
| Test-risk reason | Why this control deserves additional or normal scrutiny |
| Validation status | Untested, syntax-tested, lab-tested, idempotency-tested, assessment-verified, etc. |

## Classification definitions

- **ORIGINAL** — developed directly from the current authoritative benchmark without materially deriving the implementation from another automation project.
- **COMMON** — standard/obvious platform or Ansible technique where similar implementations naturally exist; similarity alone is not treated as inheritance.
- **ADAPTED** — another implementation materially informed this implementation, but substantial local changes were made.
- **INHERITED** — implementation substantially follows or incorporates another project's implementation.
- **NEW-CURRENT** — current requirement/implementation has no identified equivalent in the consulted prior/public automation.
More than one source may be recorded. Provenance describes implementation ancestry, not ownership of the STIG requirement itself.

## Implementation type definitions

- **REMEDIATION** — deterministic configuration change can legitimately enforce the requirement.
- **AUDIT** — automation can inspect/compare technical state but should not invent the authorization or policy boundary.
- **EVIDENCE** — compliance primarily depends on organization/process/architecture evidence not created by the role.
- **APP/EVIDENCE** — compliance depends primarily on hosted-application behavior and supporting evidence.
- Mixed forms such as **REMEDIATION/AUDIT** are allowed when the role can enforce part of a requirement but must separately validate site-owned facts.

Implementation type and provenance are independent. For example, an audit can be ORIGINAL and a remediation can be COMMON.

## Provenance-driven test scrutiny

Provenance must influence the test plan. It is not a claim that inherited code is correct or that original code is defective; it identifies where there is less prior implementation history and therefore where additional scrutiny is prudent.

Default scrutiny guidance:

| Provenance/change condition | Default scrutiny |
|---|---|
| NEW-CURRENT or ORIGINAL implementation with no prior comparable implementation | HIGH |
| ADAPTED with substantial logic/platform changes | HIGH |
| New distro/version port, path abstraction, parser, regex, XML/config mutation, or cross-file logic | HIGH |
| AUDIT/EVIDENCE logic that determines PASS/FAIL/review state | HIGH when it affects assessment conclusions |
| INHERITED with only small, understood compatibility changes | MEDIUM |
| COMMON deterministic directive with simple current-benchmark mapping | MEDIUM |
| Previously assessment-verified implementation unchanged for the same supported platform/benchmark | BASELINE |

HIGH scrutiny should normally include syntax validation, check/diff review where meaningful, positive remediation testing, idempotency testing, authoritative assessment comparison, application/service functional testing, and a deliberate negative/edge-case test. Once Anti-STIG content exists, applicable HIGH-risk controls should also receive deterministic fail -> remediate -> pass regression testing.

Scrutiny may be raised for any control. It should not be lowered merely because code was inherited from a mature public repository; current benchmark semantics, platform differences, and local modifications still require validation.

## Development workflow

For each control:

1. Start from the selected **current** DISA benchmark.
2. Record the authoritative benchmark/check/fix source.
3. Before or while consulting public automation, add that source to the ledger.
4. If source code or implementation logic materially influences the result, record its version/location/license immediately.
5. Implement the control.
6. Record material differences and the reason for them.
7. Update the ledger again whenever later testing materially changes the implementation.
8. Do not mark the implementation first-pass complete until every current control has a provenance entry.

## Existing work

Some content predates this policy and therefore requires retrospective provenance reconstruction. That reconstruction must be labeled as retrospective rather than implying contemporaneous records.

Known retrospective work includes:
- Apache HTTP Server 2.4 Server/Site initial implementation;
- earlier RHEL 10 work created through the Codex desktop workflow;
- any other pre-policy content lacking a source ledger.

Retrospective review should use repository history, source comparisons, contributor knowledge, and available development records. Uncertain provenance must be recorded as uncertain rather than guessed.

## Licensing and attribution

A current DISA requirement may independently lead multiple projects to the same obvious configuration. Do not claim inheritance based only on similarity.

When code, task structure, expressions, templates, comments, or nontrivial implementation logic are materially derived from another project, record the source and license and preserve any attribution required by that license.

## Suggested ledger location

Prefer a ledger adjacent to the implementation or in docs with an unambiguous name, for example:

- `remediation/apache/apache24/server/stig/docs/SOURCE_PROVENANCE.md`
- `remediation/apache/apache24/site/stig/docs/SOURCE_PROVENANCE.md`
- `remediation/<technology>/<product>/stig/docs/SOURCE_PROVENANCE.md`

The repository-level policy is this document. Technology-specific ledgers contain the per-control records.


## Related development guidance

- `AGENTS.md` defines the mandatory repository workflow for agents and contributors performing new lockdown or benchmark-port work.
- `docs/LOCKDOWN_LESSONS_LEARNED.md` records the Apache/Tomcat implementation lessons that explain those rules.

Read both before beginning a new technology lockdown or major benchmark revision.
