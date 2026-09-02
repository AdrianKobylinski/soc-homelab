# Change log

Notable project changes are recorded here in sanitized form. Credentials, private addressing, internal identifiers, administrative paths, and raw evidence are intentionally excluded.

## 2026-09-02

### Added

- Deployed and updated the first Windows 11 Enterprise evaluation endpoint.
- Enabled paravirtualized storage, networking, UEFI security features, and guest integration.
- Installed and enrolled Wazuh Agent 4.14.7; the endpoint reports as active.
- Installed Sysmon 15.21 with a community baseline configuration.
- Enabled collection of the Sysmon Operational channel through Wazuh Agent.
- Confirmed several process, network, termination, registry, and DNS-related Sysmon event types.
- Created and validated a local command-shell detection mapped to MITRE ATT&CK `T1059.003`.
- Completed a benign detection test and reconstructed the process chain from the interactive shell to the test commands.
- Added a sanitized Windows endpoint build record and the first detection-case report.

### Changed

- Revalidated dashboard access and all central Wazuh services during routine credential maintenance.
- Clarified that Kali Linux is a planned controlled-validation host and has not been deployed.
- Deferred Kali until network isolation and host-capacity checks are complete.
- Added endpoint-name normalization and enhanced PowerShell logging to the next-actions list.

## 2026-08-22

### Added

- Created the public SOC homelab portfolio repository.
- Added project scope, resource planning, network design, build records, and an implementation roadmap.
- Installed and updated the Proxmox virtualization foundation.
- Created and updated an Ubuntu Server VM for Wazuh.
- Installed Wazuh 4.14.7 using the official all-in-one installation method.
- Validated the Manager, Indexer, Dashboard, and Filebeat services.
- Protected locally generated credential material and excluded it from source control.
- Enabled automatic startup and created recovery points.

### Changed

- Limited the initial deployment to Wazuh and one Windows endpoint.
- Deferred additional Linux and Kali guests until capacity is reviewed and isolation is implemented.

