# RHEL 9.x Anti-STIG Test Report

## Build identity

- Repository commit:
- RHEL release:
- Image/source:
- Ansible Core:
- SCC version:
- Assessment benchmark: DISA RHEL 9 STIG V2R9
- Test date:
- Tester:

## Pre-run

- Fresh install confirmed:
- Snapshot taken:
- SSH/Ansible ping passed:
- Networking functional:
- DNF functional:
- Python functional:

## Anti-STIG run

- Playbook completed:
- Failed tasks:
- Changed count:
- Second run completed:
- Unexpected second-run changes:

## Recovery-critical postflight

- Second independent SSH login succeeded:
- Networking remained functional:
- Python remained functional:
- DNF remained functional:
- systemd-journald active:
- Host remained bootable (only verify by reboot if the test plan calls for it):

## SCC result

- PASS:
- FAIL:
- Not Applicable:
- Not Reviewed / Other:
- Score, if reported:

### Unexpected PASS findings

Record only the STIG/V-ID and the observed assessment result here. Do not copy SCAP/OVAL rule logic into implementation notes.

| STIG/V-ID | Result | Notes |
|---|---|---|

### Unexpected FAIL/errors

| STIG/V-ID or component | Result/error | Notes |
|---|---|---|

## System impact

- SSH impact:
- Network impact:
- Package-management impact:
- Logging/audit impact:
- Other functional impact:

## Recommendation

- Ready for another anti-control refinement pass:
- Preservation-boundary change requested:
- Snapshot reverted:
