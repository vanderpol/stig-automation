# Apache HTTP Server 2.4 UNIX Site V2R7 — Issues, Concerns, and Validation Notes

Last updated: 2026-09-25  
Status: **pre-team-testing / not assessment-verified**

This file records known concerns and validation boundaries for the Apache 2.4 UNIX Site STIG role.

## V-214292 — default document versus directory listing

This is a key known trap. `Options -Indexes` prevents directory listing and is useful defense-in-depth, but it does **not** satisfy the current Site check by itself. The check expects a default document such as `index.html` or equivalent in applicable document-root directories.

Current treatment remains audit/site-content oriented. Do not manufacture empty index files merely to make an assessment pass without understanding the hosted site's routing/content model.

## V-214290 — separate filesystem

Document-root filesystem placement is an architecture/deployment fact. A `findmnt` result must be compared with the Apache system/configuration filesystem as required by the current check. Automation should report the relationship, not repartition a system.

## V-214300 / V-214286 — PKI and certification-path validation

A CA file's presence does not prove that the trust anchor is DoD or DoD-approved, nor that the complete RFC 5280 validation behavior is correct. These remain evidence/architecture concerns. The role must never download or designate trust anchors on its own.

## V-214287 — private-key access

Ownership/mode inspection can identify technical exposure, but approved administrators and PKI Sponsors are organization-defined. Do not change key ownership merely to match a guessed account model.

## V-214303 — Secure cookie mutation

Global response-cookie rewriting can break application behavior or produce incorrect cookie scope. This control requires application-aware functional testing and careful handling of existing cookie attributes.

## V-214288 / V-214296 — cookie/session application behavior

Cookie Domain/Path scope and inactive-session behavior depend on the hosted application. Apache configuration can assist or audit but must not falsely claim application compliance.

## V-214297 — nonsecure-zone restrictions

Organization-defined network zones may be enforced in Apache or elsewhere. Unsafe global `Require` logic was deliberately removed. Any Apache enforcement requires explicit approved networks and site scope.

## V-214304 — ports/protocols/modules/services

Necessary/approved services and PPSM context are site-owned. Discovery can be compared with an approved inventory, but presence or absence alone does not establish authorization.

## V-214284 — containment

Directory/user/script containment changes can affect aliases, application assets, CGI, symlinks, and deployment layouts. Test real document roots and application paths rather than assuming a single conventional tree.

## V-214282 — script mappings

This overlaps in requirement theme with Server V-214244. Keep both assessment identities while avoiding contradictory or duplicated configuration mutations.

## End-user/authorization boundary

The role must not invent approved CAs, administrators, PKI Sponsors, networks, PPSM approval, application architecture, or process evidence. Required variables and evidence references support assessment but do not themselves prove authorization.

## Validation requirements

Before assessment-verified status: test each representative site/application, document-root layout, cookie/session behavior, TLS/client-certificate behavior, network restrictions, idempotency, and the authoritative current Site V2R7 assessment.

## Compliance-claim boundary

A successful Site role run is not proof that the hosted application/site is STIG compliant. Application, PKI, authorization, filesystem architecture, and process evidence remain separate.

## Anti-STIG

Negative tests should be based on a verified positive Site baseline, not on assumptions from the remediation code.
