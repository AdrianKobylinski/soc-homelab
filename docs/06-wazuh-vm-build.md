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
| QEMU Guest Agent | Enabled in Proxmox; guest package pending |
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
| Network | DHCP during installation; stable lease pending |
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

Credentials are stored privately and are not included in this repository.

## Design decisions

### Fixed 8 GB memory

Wazuh's indexer is memory intensive. Ballooning was disabled to provide predictable memory availability and avoid guest memory being reclaimed while indexing events.

### CPU type host

The lab contains only one Proxmox node, so live migration compatibility is not required. The `host` CPU type exposes the available processor features and reduces virtualization overhead.

### Expanded root volume

Ubuntu's guided LVM layout initially assigned only about half of the virtual disk to the root filesystem. The root logical volume was increased to 45 GB so Wazuh data and operating-system updates have usable space.

### Temporary trusted-network placement

The VM is initially attached to `vmbr0` for updates and deployment. Before controlled test activity begins, a second lab-facing interface will be added and endpoint traffic will be moved to an isolated bridge.

## Validation checklist

- [x] VM created with the planned CPU, memory, disk, and network settings
- [x] Ubuntu installer booted from the checksum-verified ISO
- [x] Ubuntu installation completed successfully
- [x] VM rebooted from the installed operating system
- [x] Hostname login prompt displayed
- [ ] Administrative login validated
- [ ] Network and Internet access validated
- [ ] Root filesystem capacity validated
- [ ] Operating-system updates installed
- [ ] QEMU Guest Agent installed and active
- [ ] Stable DHCP reservation configured
- [ ] Clean baseline snapshot created
