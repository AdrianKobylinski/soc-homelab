# Project scope

## Purpose

The project creates a small, reproducible SOC homelab for learning defensive monitoring and incident response. Proxmox VE provides virtualization, while Wazuh provides centralized log collection, endpoint visibility, alerting, and investigation.

## Current implementation boundary

The operational environment currently consists of the Proxmox host, an all-in-one Wazuh server, and one monitored Windows endpoint. The Linux endpoint, isolated bridge, and Kali test host are approved scope items but are **not yet deployed**.

Kali is intentionally scheduled after network isolation and a resource review. Its future role is limited to generating authorized activity against lab-owned targets; it is not required for the current Windows telemetry work.

## Learning objectives

1. Administer a small Proxmox virtualization environment.
2. Design trusted and isolated virtual networks.
3. Deploy and maintain a SIEM/XDR platform.
4. Collect Windows and Linux endpoint telemetry.
5. Investigate authentication, process, file-integrity, and security events.
6. Map detections to MITRE ATT&CK techniques.
7. Document evidence, findings, remediation, and lessons learned.
8. Restore systems safely through snapshots and backups.

## Scope and delivery state

| Component | Current state |
|---|---|
| Proxmox virtualization foundation | Operational |
| Ubuntu-based Wazuh all-in-one | Operational |
| Windows endpoint with Wazuh Agent and Sysmon | Operational |
| Detection validation and incident reporting | First case completed |
| Linux endpoint with Wazuh Agent | Planned |
| Isolated Proxmox network | Planned |
| Kali Linux against owned lab targets only | Planned after isolation |
| Build, troubleshooting, and recovery documentation | Ongoing |

## Out of scope

- Monitoring third-party systems without authorization
- Exposing Proxmox, Wazuh, or test systems directly to the Internet
- Production availability or high availability
- Full production-scale packet capture
- Malware execution outside a purpose-built isolated environment
- Resource-intensive platforms that exceed the capacity of the current host

## Constraints

- One modest Proxmox host
- Trusted management laptop and home network
- Limited concurrent VM capacity
- Kali deployment depends on isolation and a fresh resource review

## Success criteria

The lab will be considered complete when:

- Proxmox and Wazuh can be managed from the trusted laptop.
- Windows and Linux agents report to Wazuh.
- The isolated endpoint network cannot directly reach the trusted home LAN.
- Test events create searchable telemetry and expected alerts.
- A modified VM can be restored from a documented recovery point.
- Another person could reproduce the environment from this repository.

