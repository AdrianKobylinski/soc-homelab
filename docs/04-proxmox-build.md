# Proxmox build record

## Public-documentation policy

Live management addresses, credentials, unique hardware identifiers, and browser screenshots containing personal information are excluded from this public repository.

## Deployment summary

| Item | As-built value |
|---|---|
| Platform | Intel-based Dell host |
| Hypervisor | Proxmox VE 9.2.x |
| Boot mode | UEFI |
| Management addressing | Static private address, redacted publicly |
| Management URL | `https://<PROXMOX-IP>:8006` |
| Host connectivity | Wired Ethernet |
| Package repository | Proxmox VE no-subscription |

## Completed build steps

1. Downloaded the standard x86-64 Proxmox VE installer.
2. Wrote the ISO image to USB installation media.
3. Booted the Dell host in UEFI mode.
4. Installed Proxmox VE to the target disk.
5. Configured a static private management address and gateway.
6. Connected the host to the router through wired Ethernet.
7. Validated access to the web interface from the analyst laptop.
8. Disabled the subscription-only Proxmox and Ceph repositories.
9. Enabled the official Proxmox no-subscription repository.
10. Refreshed package metadata and installed available updates.

## Troubleshooting record

### USB device was not listed as bootable

**Cause:** The first installation image was an ARM64 build, while the Dell host uses an Intel x86-64 processor.

**Resolution:** Replaced it with the standard Proxmox VE x86-64 ISO and rewrote the USB drive.

**Lesson learned:** Verify CPU architecture before creating installation media.

### Management interface could not reach the router

**Symptom:** A ping to the local gateway returned `Destination Host Unreachable`.

**Cause:** The Proxmox host had no wired connection and had previously relied on Wi-Fi. Standard Proxmox Linux bridges are designed for wired interfaces.

**Resolution:** Connected the Dell host directly to a LAN port on the router using Ethernet.

**Validation:** The gateway became reachable and the web interface loaded successfully from the laptop.

### Package database update failed

**Cause:** The default enterprise repositories require a valid Proxmox subscription.

**Resolution:** Disabled `pve-enterprise` and `ceph-enterprise`, enabled `pve-no-subscription`, refreshed package metadata, and completed the upgrade.

**Validation:** Proxmox reported the package state as up to date.

## Current validation state

- [x] Host boots without installation media
- [x] Local gateway responds from the Proxmox host
- [x] Web interface is reachable from the trusted laptop
- [x] No-subscription repository is enabled
- [x] Enterprise repositories are disabled
- [x] Package state reports up to date
- [ ] Backup destination configured
- [ ] Recovery procedure tested
