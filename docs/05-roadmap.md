# Implementation roadmap

## Phase 0 — Hypervisor foundation

- [x] Install Proxmox VE
- [x] Configure static management networking
- [x] Configure package repositories
- [x] Apply available updates
- [x] Record CPU, memory, root-volume, and VM-pool capacity
- [ ] Define backup naming and retention standards

## Phase 1 — Wazuh platform

- [x] Download and checksum-verify Ubuntu Server 24.04.4 LTS AMD64
- [x] Create the Wazuh virtual machine
- [x] Install Ubuntu Server
- [x] Validate guest resources, storage, and networking
- [x] Install Ubuntu updates and QEMU Guest Agent
- [x] Configure and test a stable DHCP reservation
- [x] Create the `baseline-ubuntu-2404` snapshot
- [x] Install Wazuh 4.14.7 manager, indexer, dashboard, and Filebeat
- [x] Validate all four Wazuh services
- [ ] Validate dashboard authentication from the trusted laptop
- [ ] Protect the generated credential archive
- [ ] Apply the Wazuh repository update policy
- [ ] Create a post-install Wazuh snapshot

## Phase 2 — Windows telemetry

- [ ] Create the Windows endpoint
- [ ] Apply operating-system updates
- [ ] Install Wazuh Agent
- [ ] Install and configure Sysmon
- [ ] Validate security, process, and PowerShell telemetry
- [ ] Create a clean endpoint snapshot

## Phase 3 — Linux telemetry

- [ ] Review actual host and thin-pool capacity
- [ ] Create an Ubuntu endpoint if capacity permits
- [ ] Install Wazuh Agent
- [ ] Validate authentication, sudo, inventory, and file-integrity events
- [ ] Create a clean endpoint snapshot

## Phase 4 — Network isolation

- [ ] Create internal Proxmox bridge `vmbr1`
- [ ] Define the isolated lab subnet
- [ ] Add the Wazuh lab interface
- [ ] Move endpoints to the isolated network
- [ ] Validate separation from the trusted LAN

## Phase 5 — Controlled validation

- [ ] Review or expand storage before adding Kali
- [ ] Deploy Kali Linux
- [ ] Generate authorized test events against owned lab endpoints
- [ ] Investigate alerts in Wazuh
- [ ] Map findings to MITRE ATT&CK
- [ ] Document false positives and tuning decisions
- [ ] Produce the first incident report

## Phase 6 — Operations and recovery

- [ ] Configure scheduled backups
- [ ] Test VM restoration
- [ ] Document startup and shutdown order
- [ ] Review repository for sensitive information
- [ ] Publish a final architecture diagram and project summary
