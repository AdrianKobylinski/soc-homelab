# Change log

All notable infrastructure and documentation changes are recorded here. Live network addresses and credentials are intentionally excluded.

## 2026-08-22

### Added

- Created the public SOC homelab portfolio repository.
- Added the project scope, hardware plan, network design, Proxmox build record, and implementation roadmap.
- Documented the current Proxmox VE deployment and validation state.
- Added public-documentation rules for sanitizing network details and secrets.
- Recorded the Intel Core i5-8500 CPU, 15.42 GiB usable RAM, 67.73 GiB root volume, and 151.64 GiB LVM-Thin VM pool.
- Defined a staged deployment plan to avoid unsafe storage overcommit.
- Downloaded and checksum-verified Ubuntu Server 24.04.4 LTS AMD64.
- Created VM 100, `wazuh-server`, with 4 vCPU, 8 GB fixed RAM, and a 50 GiB disk.
- Installed and updated Ubuntu Server 24.04.4 LTS with OpenSSH Server.
- Installed and validated QEMU Guest Agent.
- Configured a router-side DHCP reservation and verified it after reboot.
- Created the pre-Wazuh snapshot `baseline-ubuntu-2404`.
- Added the detailed Wazuh VM build record.

### Changed

- Limited the initial deployment to Wazuh and one Windows endpoint.
- Deferred Ubuntu and Kali guests until actual capacity is reviewed or storage is expanded.
- Expanded the Ubuntu root logical volume from the guided default to 45 GB.

### Completed before repository creation

- Installed Proxmox VE 9.2.x on the Dell host.
- Configured static private management networking.
- Replaced an incompatible ARM64 installer with the correct x86-64 image.
- Connected the Proxmox host through wired Ethernet.
- Enabled the no-subscription repository and completed system updates.
