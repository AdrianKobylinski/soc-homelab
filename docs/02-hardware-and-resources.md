# Hardware and resource plan

## Physical inventory

| Component | Confirmed information | Purpose |
|---|---|---|
| Virtualization host | Dell system, Intel CPU, 6 logical CPUs, 15.42 GiB usable RAM | Proxmox VE and all lab VMs |
| Proxmox storage | 208.95 GiB aggregate configured storage | Host, ISO images, VM disks, and snapshots |
| Router | Home router, details redacted publicly | Trusted LAN and Internet access |
| Analyst workstation | Laptop connected to the home router | Administration and investigation |
| Switch | Not required for the initial design | Possible future expansion |
| Access point | Not required if router Wi-Fi is used | Possible future expansion |

The exact Dell model, CPU model, physical-disk model, and unique hardware identifiers are not yet recorded publicly. Serial numbers and service tags will never be published.

## Host resource strategy

Proxmox must retain enough memory for the host and storage services. The first version of the lab therefore keeps Wazuh online and runs only the endpoint required for the current exercise.

| VM | vCPU | RAM | Initial storage | Runtime policy |
|---|---:|---:|---:|---|
| Wazuh | 4 | 8 GB fixed | 50 GB | Normally online |
| Windows endpoint | 2 | 4 GB | 64 GB | Start when required |
| Ubuntu endpoint | 1–2 | 2 GB | 20 GB | Start when required |
| Kali Linux | 2 | 2–3 GB | 25–30 GB | Start only for isolated tests |

CPU overcommit is acceptable for this low-load training environment. RAM overcommit will be avoided.

## Capacity assessment

The planned maximum virtual-disk allocation is approximately 159–164 GB. The host reports 208.95 GiB of aggregate configured storage, but this value may combine multiple Proxmox storage pools. The capacity of the VM storage pool must be confirmed before all machines are deployed.

Space must also remain available for:

- the Proxmox operating system
- ISO images
- Wazuh log growth
- snapshots
- temporary installation files

Backups should ultimately be stored outside the only physical host. A single internal disk is not a backup.

## Operating rules for the 16 GB host

1. Keep Wazuh online during monitoring exercises.
2. Run only the endpoint required for the current scenario.
3. Stop Kali when it is not actively used.
4. Avoid memory overcommit and aggressive ballooning for Wazuh.
5. Monitor both `local` and `local-lvm` capacity before creating snapshots.
6. Delete unused ISO images after verified installation media is no longer required.
7. Add external backup storage before treating the lab as recoverable.

## Capacity upgrade path

The most useful future upgrades are:

1. **32 GB RAM or more** — allows more endpoint VMs to run concurrently.
2. **Additional SSD storage** — provides more room for Wazuh retention and snapshots.
3. **Separate backup destination** — protects against failure of the Proxmox host disk.
