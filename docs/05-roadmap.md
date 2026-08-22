# Implementation roadmap

## Phase 0 — Hypervisor foundation

- [x] Install Proxmox VE
- [x] Configure static management networking
- [x] Configure package repositories
- [x] Apply available updates
- [ ] Record complete hardware and storage inventory
- [ ] Define snapshot and backup naming standards

## Phase 1 — Wazuh platform

- [ ] Upload Ubuntu Server 24.04 LTS ISO
- [ ] Create the Wazuh virtual machine
- [ ] Install and update Ubuntu Server
- [ ] Assign a stable address
- [ ] Install Wazuh manager, indexer, and dashboard
- [ ] Validate dashboard access
- [ ] Create a clean deployment snapshot

## Phase 2 — Windows telemetry

- [ ] Create the Windows endpoint
- [ ] Apply operating-system updates
- [ ] Install Wazuh Agent
- [ ] Install and configure Sysmon
- [ ] Validate security, process, and PowerShell telemetry
- [ ] Create a clean endpoint snapshot

## Phase 3 — Linux telemetry

- [ ] Create an Ubuntu endpoint
- [ ] Install Wazuh Agent
- [ ] Validate authentication, sudo, inventory, and file-integrity events
- [ ] Create a clean endpoint snapshot

## Phase 4 — Network isolation

- [ ] Create internal Proxmox bridge `vmbr1`
- [ ] Define the `10.10.10.0/24` lab subnet
- [ ] Add the Wazuh lab interface
- [ ] Move endpoints to the isolated network
- [ ] Validate separation from the trusted LAN

## Phase 5 — Controlled validation

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
