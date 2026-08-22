# Hardware and resource plan

## Physical inventory

| Component | Current information | Purpose |
|---|---|---|
| Virtualization host | Dell system, Intel CPU, 16 GB RAM | Proxmox VE and all lab VMs |
| Router | Home router, management gateway | Trusted LAN and Internet access |
| Analyst workstation | Laptop connected to the home router | Administration and investigation |
| Switch | Not required for the initial design | Possible future expansion |
| Access point | Not required if router Wi-Fi is used | Possible future expansion |

The exact Dell model, CPU model, storage capacity, and network-interface details will be added after inventory collection.

## Host resource strategy

Proxmox must retain enough memory for the host and storage services. The first version of the lab therefore keeps Wazuh online and runs only the endpoint required for the current exercise.

| VM | vCPU | RAM | Storage | Runtime policy |
|---|---:|---:|---:|---|
| Wazuh | 4 | 8 GB fixed | 50–80 GB | Normally online |
| Windows endpoint | 2 | 4 GB | 64 GB | Start when required |
| Ubuntu endpoint | 1–2 | 2 GB | 25 GB | Start when required |
| Kali Linux | 2 | 2–3 GB | 35–40 GB | Start only for isolated tests |

CPU overcommit is acceptable for this low-load training environment. RAM overcommit will be avoided.

## Storage planning

Estimated planned allocation is approximately 180–220 GB, excluding:

- Proxmox system storage
- snapshots
- backups
- ISO images
- future log growth

The final virtual-disk sizes will be selected only after the physical storage capacity and current Proxmox allocation are confirmed.

## Capacity upgrade path

The most useful future upgrade is 32 GB RAM or more. This would allow Wazuh, Windows, Ubuntu, Kali, and a dedicated virtual firewall to run concurrently with a safer memory margin.
