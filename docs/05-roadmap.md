# Implementation roadmap

A checked item is implemented and validated. An unchecked item is planned; appearance in this roadmap does not mean the component is already installed.

## Phase 0 — Hypervisor foundation

- [x] Install and update Proxmox VE
- [x] Configure management networking
- [x] Record resource capacity
- [ ] Define backup naming and retention standards

## Phase 1 — Wazuh platform

- [x] Create and update the Ubuntu Server VM
- [x] Validate guest resources, storage, and networking
- [x] Install Wazuh 4.14.7 all-in-one
- [x] Validate Manager, Indexer, Dashboard, and Filebeat
- [x] Protect locally generated credential material
- [x] Prevent unplanned independent component upgrades
- [x] Enable automatic startup and create recovery points
- [x] Revalidate services and dashboard authentication after credential maintenance

## Phase 2 — Windows telemetry

- [x] Create and install the Windows 11 endpoint
- [x] Apply operating-system and Defender updates
- [x] Install paravirtualized drivers and guest integration
- [x] Create clean recovery points
- [x] Install and enroll Wazuh Agent 4.14.7
- [x] Confirm the endpoint reports as active
- [x] Install Sysmon 15.21 with a community baseline
- [x] Forward the Sysmon Operational channel through Wazuh Agent
- [x] Validate process telemetry and custom-rule alerting
- [ ] Normalize the Windows computer name and revalidate after reboot
- [ ] Enable and validate enhanced PowerShell logging
- [ ] Confirm a current post-Sysmon recovery point

## Phase 3 — Linux telemetry

- [ ] Review current host capacity
- [ ] Create an Ubuntu endpoint if capacity permits
- [ ] Install Wazuh Agent
- [ ] Validate authentication, sudo, inventory, and file-integrity events
- [ ] Create a clean recovery point

## Phase 4 — Network isolation

- [ ] Create an internal Proxmox bridge
- [ ] Define an isolated lab subnet
- [ ] Add the required Wazuh lab interface
- [ ] Move endpoints to the isolated network
- [ ] Validate separation from the trusted LAN

## Phase 5 — Controlled validation and attack emulation

- [x] Generate an authorized benign command-shell test
- [x] Create and validate a local Wazuh detection
- [x] Investigate the resulting Sysmon process-creation alert
- [x] Reconstruct the process chain using indexed telemetry and live response
- [x] Map the detection to MITRE ATT&CK `T1059.003`
- [x] Produce the first detection-case report
- [ ] Review capacity before adding Kali
- [ ] Complete network isolation before adding Kali
- [ ] Deploy Kali Linux as a controlled test source
- [ ] Generate additional authorized scenarios against owned lab endpoints
- [ ] Document false positives and tuning decisions

## Phase 6 — Operations and recovery

- [ ] Configure scheduled backups
- [ ] Test VM restoration
- [ ] Document startup and shutdown order
- [ ] Review the repository for sensitive information
- [ ] Publish a final architecture diagram and project summary

