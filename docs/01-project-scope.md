# Project scope

## Purpose

The project creates a small, reproducible SOC homelab for learning defensive monitoring and incident response. Proxmox VE provides virtualization, while Wazuh will provide centralized log collection, endpoint visibility, alerting, and investigation.

## Learning objectives

1. Administer a small Proxmox virtualization environment.
2. Design trusted and isolated virtual networks.
3. Deploy and maintain a SIEM/XDR platform.
4. Collect Windows and Linux endpoint telemetry.
5. Investigate authentication, process, file-integrity, and security events.
6. Map detections to MITRE ATT&CK techniques.
7. Document evidence, findings, remediation, and lessons learned.
8. Restore systems safely through snapshots and backups.

## In scope

- Proxmox VE host installation and configuration
- Ubuntu Server 24.04 LTS
- Wazuh manager, indexer, and dashboard
- Windows endpoint with Wazuh Agent and Sysmon
- Linux endpoint with Wazuh Agent
- Isolated virtual network for controlled exercises
- Kali Linux used only against owned lab targets
- Detection validation and incident-report exercises
- Build, troubleshooting, and recovery documentation

## Out of scope

- Monitoring third-party systems without authorization
- Exposing Proxmox, Wazuh, or test systems directly to the Internet
- Production availability or high availability
- Full production-scale packet capture
- Malware execution outside a purpose-built isolated environment
- Security Onion deployment on the current 16 GB host

## Constraints

- One Intel-based Dell Proxmox host
- 16 GB physical RAM
- Single home router and trusted management laptop
- Limited concurrent VM capacity
- Storage capacity is still to be confirmed

## Success criteria

The initial lab will be considered operational when:

- Proxmox and Wazuh can be managed from the trusted laptop.
- Windows and Linux agents report to Wazuh.
- The isolated endpoint network cannot directly reach the trusted home LAN.
- Test events create searchable telemetry and expected alerts.
- A failed or modified VM can be restored from a documented recovery point.
- Another person could reproduce the environment from this repository.
