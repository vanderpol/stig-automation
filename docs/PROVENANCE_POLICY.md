# Provenance and Source Ledger Policy

## Mandatory rule for all future work

Every implementation, remediation role, SCAP/OVAL check, Anti-STIG test, benchmark port, or substantial modification in this repository must maintain a provenance/source ledger **while the work is being created**.

Provenance is not an optional after-the-fact documentation task. A work item is not considered implementation-complete until its ledger is updated.

This rule applies to new work and to changes of existing content, regardless of whether the work is performed in ChatGPT, Codex, an IDE, by hand, or by another contributor.

## Why

STIG automation often resembles existing public implementations because the benchmark prescribes the same underlying configuration. Similarity alone does not prove derivation. Conversely, adapted or inherited implementation should not lose its history.

Recording provenance at implementation time lets maintainers:
- distinguish work derived directly from current DISA requirements from work influenced by another project;
- identify inherited/adapted code and applicable licenses/attribution;
- understand what was changed and why;
- evaluate upstream fixes and future benchmark changes;
- identify controls that appear genuinely new for the current benchmark;
- avoid reconstructing development history after the fact.

## Required ledger fields

Each current V-ID/control must record, as applicable:

| Field | Requirement |
|---|---|
| V-ID/control | Current benchmark identifier |
| Benchmark | Version/release used as implementation authority |
| Classification | ORIGINAL, COMMON, ADAPTED, INHERITED, NEW-CURRENT, or EVIDENCE/AUDIT |
| Primary authority | Current DISA STIG/check/fix source |
| Reference source(s) | Public repository/project/document consulted |
| Source version | Tag, release, or commit when available |
| Source location | Role/task/file/control identifier or URL/reference |
| License | License of materially used source |
| Material used | What concept/code/approach informed the implementation |
| Local changes | What this repository changed from the source |
| Reason | Why the local implementation differs |
| Contributor/date | Useful development-history context |

## Classification definitions

- **ORIGINAL** — developed directly from the current authoritative benchmark without materially deriving the implementation from another automation project.
- **COMMON** — standard/obvious platform or Ansible technique where similar implementations naturally exist; similarity alone is not treated as inheritance.
- **ADAPTED** — another implementation materially informed this implementation, but substantial local changes were made.
- **INHERITED** — implementation substantially follows or incorporates another project's implementation.
- **NEW-CURRENT** — current requirement/implementation has no identified equivalent in the consulted prior/public automation.
- **EVIDENCE/AUDIT** — repository implementation primarily performs evidence collection, validation, or assessment because deterministic remediation would invent organization/application policy.

More than one source may be recorded. The classification describes implementation provenance, not ownership of the STIG requirement itself.

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
- `docs/<technology>_SOURCE_PROVENANCE.md`

The repository-level policy is this document. Technology-specific ledgers contain the per-control records.
