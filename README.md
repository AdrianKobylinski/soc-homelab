# SOC Homelab

A defensive security homelab built on Proxmox VE for SOC monitoring, detection engineering, incident investigation, and incident response practice.

> **Project status:** In progress — Ubuntu Wazuh VM installed, guest validation pending.

## Project goals

- Build a reproducible virtualized SOC environment.
- Collect and analyze Windows and Linux endpoint telemetry.
- Deploy Wazuh as the central SIEM/XDR platform.
- Practice alert triage, investigation, detection tuning, and reporting.
- Safely generate test events inside an isolated lab network.
- Document design decisions, implementation steps, validation, and troubleshooting.

## Current status

- [x] Installed Proxmox VE 9.2.x on an Intel-based Dell host
- [x] Configured static management networking
- [x] Enabled the official no-subscription repository
- [x] Updated the Proxmox host
- [x] Validated remote web management
- [x] Recorded host and storage capacity
- [x] Downloaded and checksum-verified Ubuntu Server 24.04.4 LTS AMD64
- [x] Created and installed the Ubuntu VM for Wazuh
- [ ] Validate and update the Ubuntu guest
- [ ] Install the Wazuh all-in-one stack
- [ ] Deploy a Windows monitored endpoint
- [ ] Create an isolated virtual lab network
- [ ] Add Linux and Kali systems when capacity permits
- [ ] Build and document detection scenarios

## Planned architecture

```mermaid
flowchart LR
    Laptop["Analyst laptop"] -->|"HTTPS management"| Router["Home router"]
    Router -->|"Ethernet"| PVE["Dell / Proxmox VE"]
    PVE --> Wazuh["Wazuh SIEM/XDR"]
    PVE --> Endpoints["Windows and Linux endpoints"]
    PVE --> Kali["Kali test host"]
    Kali -->|"Controlled lab activity"| Endpoints
    Endpoints -->|"Logs and telemetry"| Wazuh
    Wazuh -->|"Alerts and investigation"| Laptop
```

The endpoint and test systems will later be moved to an isolated Proxmox bridge. The Wazuh dashboard and Proxmox management interface will remain reachable only from the trusted home network.

## Confirmed host capacity

| Resource | Confirmed capacity |
|---|---|
| CPU | Intel Core i5-8500, 6 cores/6 threads |
| RAM | 15.42 GiB usable |
| VM storage | 151.64 GiB LVM-Thin |
| Host/ISO storage | 67.73 GiB root volume |

## Initial deployment plan

| System | Role | vCPU | RAM | Disk |
|---|---|---:|---:|---:|
| Wazuh on Ubuntu Server 24.04 | SIEM, indexing, alerting, dashboard | 4 | 8 GB | 50 GB |
| Windows endpoint | Windows telemetry, Sysmon, Wazuh agent | 2 | 4 GB | 64 GB |

Ubuntu and Kali guests are planned for later phases after reviewing actual storage and memory usage. Because the host has 16 GB of RAM, only machines required for the current exercise will run at the same time.

## Documentation

- [Project scope](docs/01-project-scope.md)
- [Hardware and resource plan](docs/02-hardware-and-resources.md)
- [Network design](docs/03-network-design.md)
- [Proxmox build record](docs/04-proxmox-build.md)
- [Implementation roadmap](docs/05-roadmap.md)
- [Wazuh VM build record](docs/06-wazuh-vm-build.md)
- [Change log](CHANGELOG.md)

## Safety

This environment is intended exclusively for authorized defensive-security education. Test activity will be limited to systems owned by the lab operator and placed inside the isolated lab network. No lab service will be exposed directly to the public Internet.

## Repository policy

Secrets, credentials, private keys, VM images, ISO files, and sensitive screenshots are excluded from this repository. Screenshots are reviewed and cropped before publication.
