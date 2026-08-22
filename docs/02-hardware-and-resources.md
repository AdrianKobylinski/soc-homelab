# Hardware and resource plan

## Physical inventory

| Component | Confirmed information | Purpose |
|---|---|---|
| Virtualization host | Dell system with Intel Core i5-8500, 6 cores/6 threads at 3.00 GHz | Proxmox VE and all lab VMs |
| Memory | 15.42 GiB usable RAM, 8 GiB swap | Host and guest memory |
| Proxmox root volume | 67.73 GiB, approximately 5.74 GiB used during inventory | Host OS and ISO storage |
| Proxmox VM pool | 151.64 GiB LVM-Thin, empty during inventory | VM and container disks |
| Router | Home router, details redacted publicly | Trusted LAN and Internet access |
| Analyst workstation | Laptop connected to the home router | Administration and investigation |
| Switch and separate AP | Not required for the initial design | Possible future expansion |

Unique hardware identifiers, serial numbers, service tags, and live management addresses are not published.

## Host resource strategy

Proxmox must retain enough memory for the host and storage services. The first version of the lab therefore keeps Wazuh online and runs only the endpoint required for the current exercise.

| VM | vCPU | RAM | Initial disk | Deployment decision |
|---|---:|---:|---:|---|
| Wazuh | 4 | 8 GB fixed | 50 GB | Phase 1 |
| Windows endpoint | 2 | 4 GB | 64 GB | Phase 2 |
| Ubuntu endpoint | 1–2 | 2 GB | 20 GB | Add after capacity review |
| Kali Linux | 2 | 2–3 GB | 20–25 GB | Postpone until storage review or expansion |

CPU overcommit is acceptable for this low-load training environment. RAM overcommit will be avoided.

## Storage decision

The `local-lvm` pool provides 151.64 GiB for VM disks.

| Deployment stage | Maximum allocated VM disks | Remaining pool capacity |
|---|---:|---:|
| Wazuh only | 50 GB | approximately 101.64 GiB |
| Wazuh + Windows | 114 GB | approximately 37.64 GiB |
| Add Ubuntu endpoint | 134 GB | approximately 17.64 GiB |
| Add Kali at 20 GB | 154 GB | exceeds the physical pool |

The values mix decimal GB requested by VM disks with GiB reported by Proxmox, so they are planning estimates rather than byte-exact calculations.

The initial approved deployment is Wazuh plus Windows. Ubuntu will be added only after reviewing actual thin-pool usage. Kali will require additional storage, removal of an unused VM, or a deliberately revised disk plan.

## Storage operating rules

1. Store installation ISOs on `local`, not `local-lvm`.
2. Keep substantial free space in the LVM-Thin pool.
3. Monitor actual usage before and after snapshots.
4. Never allow the thin pool to reach 100 percent usage.
5. Delete unused ISO images after installations are verified.
6. Store backups outside the only physical Proxmox host.
7. Treat snapshots as temporary recovery points, not backups.

## Operating rules for the 16 GB host

1. Keep Wazuh online during monitoring exercises.
2. Run only the endpoint required for the current scenario.
3. Avoid RAM overcommit and aggressive ballooning for Wazuh.
4. Shut down unused guest systems.
5. Review host memory before starting another VM.

## Capacity upgrade path

The most useful future upgrades are:

1. **32 GB RAM or more** — allows more endpoint VMs to run concurrently.
2. **Additional SSD storage** — provides room for Kali, retention, and snapshots.
3. **Separate backup destination** — protects against failure of the Proxmox host disk.
