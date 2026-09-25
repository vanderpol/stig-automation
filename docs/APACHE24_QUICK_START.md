# Apache 2.4 STIG Remediation — Novice Quick Start

This is the starting point for a first-time user. Do not begin by editing files under `remediation/`.

## What you are applying

There are two separate current Apache benchmarks:

1. **Server V3R3** — hardens the Apache server instance.
2. **Site V2R7** — evaluates/hardens each hosted web site/application.

Apply and test **Server first, then Site**. If one Apache server hosts multiple applications, the Server role is applied to the server, while each application may need its own Site profile and Site assessment.

A successful Ansible run does not by itself prove STIG compliance. Some requirements need organization/application decisions or evidence.

## Before you begin

Use a representative **non-production test server** first. Back up/snapshot it.

The control machine running Ansible needs:
- Git;
- Ansible Core 2.14 or newer;
- SSH access to the target;
- an account that can use sudo/become on the target.

The target must already have Apache HTTP Server 2.4 installed. Supported first-pass targets are RHEL 8/9/10 and Ubuntu 22.04/24.04/26.04.

All commands below are run from the repository root.

## Step 1 — Create your inventory

Copy the example:

```bash
cp inventories/lab/hosts.apache24.example.yml inventories/lab/hosts.yml
```

Edit `inventories/lab/hosts.yml`. Replace the example address and SSH user with your test server.

For a server that will receive both Server and Site remediation, put the same host in both groups:

```yaml
---
all:
  children:
    apache24:
      hosts:
        apache-test:
          ansible_host: 192.0.2.20
          ansible_user: ansible
    apache24_site:
      hosts:
        apache-test:
          ansible_host: 192.0.2.20
          ansible_user: ansible
```

Use your real address. The `192.0.2.x` addresses in examples are documentation placeholders.

## Step 2 — Create the Server profile

Copy:

```bash
cp inventories/lab/group_vars/apache24.yml.example inventories/lab/group_vars/apache24.yml
```

Edit `apache24.yml`.

At minimum, replace `apache24_stig_listen` with the **approved explicit IP:port** on which this Apache server should listen. Do not copy the example address unchanged.

Do not guess values just to make preflight green. If your organization must approve a value, obtain that decision first.

## Step 3 — Verify Ansible can reach the server

```bash
ansible apache24 -m ping
```

If this fails, fix SSH, inventory, DNS/address, credentials, or sudo access before continuing.

## Step 4 — Run Server preflight

```bash
ansible-playbook playbooks/apache24_server_preflight.yml
```

Look near the end for the readiness summary:

- **READY** — required profile inputs known to the role are present; this does not mean the system already passes the STIG.
- **SITE INPUT REQUIRED** — you must supply an organization/application value.
- **EVIDENCE REQUIRED** — the technical role cannot manufacture the required documentation, authorization, architecture, or operational evidence.

Resolve applicable items before remediation.

## Step 5 — Preview Server changes

```bash
ansible-playbook playbooks/apache24_server_stig.yml --check --diff
```

Read the output. Check mode is a preview and cannot perfectly simulate every command/module. Do not treat it as proof that the real run will succeed.

## Step 6 — Apply Server remediation

```bash
ansible-playbook playbooks/apache24_server_stig.yml
```

The role runs Apache `configtest`. Afterward, test the real web application yourself: pages, authentication, TLS, reverse proxy/load balancer behavior, logging, and anything else the application uses.

Run the playbook a second time:

```bash
ansible-playbook playbooks/apache24_server_stig.yml
```

Unexpected changes on every run should be investigated.

## Step 7 — Create the Site profile

Only after the Server baseline is working, copy:

```bash
cp inventories/lab/group_vars/apache24_site.yml.example inventories/lab/group_vars/apache24_site.yml
```

Edit it for the hosted application.

You must supply the real document root. If PKI/client certificates apply, the organization must supply its approved CA/trust material and evidence. **Do not put private keys or passwords in this repository.**

If the server hosts multiple applications with different security decisions, create separate inventory groups/group-variable profiles rather than forcing all sites to share one profile.

## Step 8 — Run Site preflight and preview

```bash
ansible apache24_site -m ping
ansible-playbook playbooks/apache24_site_preflight.yml
ansible-playbook playbooks/apache24_site_stig.yml --check --diff
```

Resolve all applicable Site input/evidence items before applying.

## Step 9 — Apply Site remediation

```bash
ansible-playbook playbooks/apache24_site_stig.yml
```

Then test the hosted application, especially TLS/client certificates, cookies/sessions, authentication, document access, redirects, and application-specific URLs.

Run the Site playbook a second time to check idempotency.

## Step 10 — Perform the authoritative assessment

Run the current authoritative assessments for:
- Apache Server 2.4 UNIX Server STIG **V3R3**;
- Apache Server 2.4 UNIX Site STIG **V2R7**.

Do not use an older checklist to decide what the automation should implement.

Record every PASS, FAIL, N/A, and manual/evidence result. Ansible output is supporting information, not the final compliance determination.

## What you must do yourself

The automation cannot legitimately decide or create:
- approved DoD/DoD-approved PKI trust anchors and CA authorization;
- certificate/private-key authorization;
- application/session architecture and behavior;
- approved administrative accounts;
- organization-defined network zones;
- PPSM approvals;
- disaster-recovery/baseline procedures;
- patch/vendor-support evidence;
- logging/security-integration evidence;
- other organization-defined approvals.

The preflight output and the Server/Site user guides explain these in more detail.

## Stop conditions

Do not continue blindly if:
- preflight reports a required value you do not understand;
- `--check --diff` proposes an unexpected application/configuration change;
- Apache `configtest` fails;
- the application fails functional testing;
- you do not know whether a site-specific value is authorized.

Resolve the issue or obtain the site decision first.

## Next documents

- `docs/APACHE24_SERVER_USER_GUIDE.md` — detailed Server responsibilities.
- `docs/APACHE24_SITE_USER_GUIDE.md` — detailed Site responsibilities.
- `remediation/apache/apache24/server/stig/docs/CONTROL_MATRIX.md` — Server V-ID ledger.
- `remediation/apache/apache24/site/stig/docs/CONTROL_MATRIX.md` — Site V-ID ledger.
- `docs/APACHE24_DUPLICATE_REVIEW.md` — current duplicate candidates.
- `docs/APACHE24_FIRST_PASS_STATUS.md` — implementation/test status.
