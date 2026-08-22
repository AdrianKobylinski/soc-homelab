# Network design

## Public-documentation policy

The public repository intentionally does not contain the real home-LAN gateway, Proxmox management address, Wi-Fi information, or device identifiers. The ranges below use RFC 5737 documentation addresses and are not the live network configuration.

| Documentation range | Represents |
|---|---|
| `192.0.2.0/24` | Trusted management network example |
| `198.51.100.0/24` | Isolated SOC lab network example |

The exact as-built addresses are retained only in private operator notes.

## Phase 1: trusted management network

The first deployment phase uses the existing trusted LAN for installation, updates, and administration.

| Component | Public example | Function |
|---|---|---|
| Trusted LAN | `192.0.2.0/24` | Management network |
| Router | `192.0.2.1` | Default gateway and DNS forwarder |
| Proxmox VE | `192.0.2.50` | Hypervisor management |
| Proxmox bridge | `vmbr0` | Physical Ethernet bridge |

The Proxmox host uses wired Ethernet. The analyst laptop may use the router's Wi-Fi while remaining on the trusted subnet.

## Phase 2: isolated SOC lab network

Before controlled test activity begins, an internal bridge will be created without a physical uplink.

| Component | Public example | Function |
|---|---|---|
| Lab network | `198.51.100.0/24` | Isolated VM network |
| Wazuh lab interface | `198.51.100.10` | Agent and telemetry destination |
| Windows endpoint | `198.51.100.20` | Monitored workstation |
| Ubuntu endpoint | `198.51.100.30` | Monitored Linux server |
| Kali Linux | `198.51.100.40` | Controlled test host |
| Proxmox bridge | `vmbr1` | Internal-only virtual switch |

These are portfolio examples, not live addresses. Final local values are recorded privately.

## Segmentation principles

- Proxmox management remains on `vmbr0`.
- Kali and monitored endpoints move to `vmbr1` before test activity.
- Wazuh receives a lab-facing interface so agents can send telemetry.
- IP forwarding is not enabled on the Wazuh server.
- No router port-forwarding rules expose the lab.
- Internet access for isolated machines is introduced only through an explicitly documented controlled method, if required.

## Validation checks

1. The trusted laptop can reach the Proxmox web interface.
2. Proxmox can reach its default gateway.
3. Lab endpoints can reach the Wazuh lab interface.
4. Kali cannot directly reach trusted home-LAN systems.
5. No Proxmox or Wazuh management port is reachable from the public Internet.
