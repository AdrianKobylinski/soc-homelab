# Wazuh VM build record

## Purpose

This VM will host the Wazuh manager, indexer, and dashboard in an all-in-one deployment for a small SOC training environment.

## Proxmox configuration

| Setting | As-built value |
|---|---|
| VM ID | 100 |
| VM name | `wazuh-server` |
| Guest OS | Ubuntu Server 24.04.4 LTS AMD64 |
| Machine type | Default i440fx |
| Firmware | SeaBIOS |
| SCSI controller | VirtIO SCSI single |
| QEMU Guest Agent | Enabled in Proxmox and active in the guest |
| CPU | 1 socket, 4 cores, type `host` |
| Memory | 8192 MiB fixed |
| Ballooning | Disabled |
| Disk | 50 GiB on `local-lvm` |
| Disk interface | SCSI |
| Discard | Enabled |
| IO thread | Enabled |
| Network model | VirtIO |
| Initial bridge | `vmbr0` |
| Proxmox firewall flag | Enabled |
| Start at boot | Disabled during initial build |

## Ubuntu installation choices

| Setting | Choice |
|---|---|
| Installer | Ubuntu Server 24.04.4 LTS, installer update applied |
| Keyboard | English (US) |
| Installation type | Standard Ubuntu Server |
| Third-party drivers | Not selected |
| Network | DHCP with a router-side reservation |
| Proxy | None |
| Archive mirror | Regional Ubuntu archive |
| Storage | Entire 50 GiB virtual disk with LVM |
| Root logical volume | 45 GB |
| Boot partition | 2 GB |
| LVM free space | Approximately 3 GB |
| Disk encryption | Not enabled |
| Ubuntu Pro | Skipped |
| OpenSSH Server | Installed |
| SSH password authentication | Temporarily enabled |
| Featured snaps | None |
| Hostname | `wazuh-server` |
| Administrative user | `socadmin` |

Credentials, the live IP address, and the virtual NIC MAC address are stored privately and are not included in this repository.

## Design decisions

### Fixed 8 GB memory

Wazuh's indexer is memory intensive. Ballooning was disabled to provide predictable memory availability and avoid guest memory being reclaimed while indexing events.

### CPU type host

The lab contains only one Proxmox node, so live migration compatibility is not required. The `host` CPU type exposes the available processor features and reduces virtualization overhead.

### Expanded root volume

Ubuntu's guided LVM layout initially assigned only about half of the virtual disk to the root filesystem. The root logical volume was increased to 45 GB so Wazuh data and operating-system updates have usable space.

### Router-side DHCP reservation

The VM retains DHCP configuration, while the router maps its virtual MAC address to a stable private address. This avoids hard-coding local gateway and DNS details inside the guest while keeping the Wazuh address stable.

### Temporary trusted-network placement

The VM is initially attached to `vmbr0` for updates and deployment. Before controlled test activity begins, a second lab-facing interface will be added and endpoint traffic will be moved to an isolated bridge.

## Baseline recovery point

| Snapshot | State captured |
|---|---|
| `baseline-ubuntu-2404` | Clean and updated Ubuntu, active QEMU Guest Agent, stable DHCP reservation, before Wazuh installation |

The snapshot excludes VM RAM and is intended as a temporary rollback point, not as a backup.

## Validation checklist

- [x] VM created with the planned CPU, memory, disk, and network settings
- [x] Ubuntu installer booted from the checksum-verified ISO
- [x] Ubuntu installation completed successfully
- [x] VM rebooted from the installed operating system
- [x] Administrative login validated
- [x] Network, gateway, and routing validated
- [x] Root filesystem capacity validated
- [x] Operating-system updates installed
- [x] QEMU Guest Agent installed and active
- [x] Stable DHCP reservation configured and tested after reboot
- [x] Clean baseline snapshot created
