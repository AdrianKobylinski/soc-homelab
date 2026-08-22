# Change log

All notable infrastructure and documentation changes are recorded here. Live network addresses and credentials are intentionally excluded.

## 2026-08-22

### Added

- Created the public SOC homelab portfolio repository.
- Added the project scope, hardware plan, network design, Proxmox build record, and implementation roadmap.
- Documented the current Proxmox VE deployment and validation state.
- Added public-documentation rules for sanitizing network details and secrets.
- Recorded 6 logical CPUs, 15.42 GiB usable RAM, and 208.95 GiB aggregate Proxmox storage.
- Adjusted the initial VM storage plan to fit the current host more safely.

### Completed before repository creation

- Installed Proxmox VE 9.2.x on the Dell host.
- Configured static private management networking.
- Replaced an incompatible ARM64 installer with the correct x86-64 image.
- Connected the Proxmox host through wired Ethernet.
- Enabled the no-subscription repository and completed system updates.
