# Wazuh installation record

## Deployment summary

| Item | As-built value |
|---|---|
| Deployment type | All-in-one |
| Wazuh version | 4.14.7 |
| Operating system | Ubuntu Server 24.04.4 LTS |
| Installation method | Official Wazuh installation assistant |
| Dashboard protocol | HTTPS |
| Dashboard port | 443 |
| Credential storage | Private password manager; excluded from GitHub |
| Post-install snapshot | `wazuh-4147-installed` |

The all-in-one deployment places the Wazuh manager, indexer, dashboard, and Filebeat on the same VM. This is appropriate for the small number of endpoints planned for the lab.

## Installation procedure

The official assistant was downloaded and executed with administrative privileges:

```bash
curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh
sudo bash ./wazuh-install.sh -a
```

The `-a` option selected the all-in-one installation.

## Installation milestones observed

- Hardware requirements check passed.
- Wazuh repository was added.
- Root, administrator, indexer, Filebeat, and dashboard certificates were generated.
- The protected `wazuh-install-files.tar` credential archive was created.
- Wazuh Indexer was installed and its cluster initialized.
- Wazuh Manager was installed.
- Filebeat and the Wazuh Dashboard were configured.
- The installer returned `Installation finished`.

## Service validation

| Service | Validation command | Result |
|---|---|---|
| Wazuh Manager | `systemctl is-active wazuh-manager` | `active` |
| Wazuh Indexer | `systemctl is-active wazuh-indexer` | `active` |
| Wazuh Dashboard | `systemctl is-active wazuh-dashboard` | `active` |
| Filebeat | `systemctl is-active filebeat` | `active` |

The four services remained active after the final Ubuntu package update.

## Dashboard validation

- The dashboard loaded over HTTPS from the trusted analyst laptop.
- The expected self-signed certificate warning was handled locally.
- Administrator authentication succeeded.
- The Overview page loaded and displayed platform alerts.
- The initial registered-agent count was zero, as expected before endpoint deployment.
- No dashboard credentials or live network addresses were captured in the public documentation.

## Credential handling

The assistant generated the dashboard administrator password and a credential archive containing certificates, cluster keys, and service passwords.

Implemented controls:

- The archive was moved to `/root/wazuh-install-files.tar`.
- Ownership was set to `root:root`.
- Permissions were set to `600`.
- The administrator password was stored privately.
- Screenshots containing passwords or tokens are excluded from the repository.

## Repository update policy

After all components were installed and validated, the Wazuh APT source was commented out and the package index was refreshed. This follows Wazuh guidance and prevents unplanned independent component upgrades.

Future Wazuh upgrades must be deliberate: create a backup or snapshot, review the supported upgrade path, re-enable the repository temporarily, upgrade compatible components together, validate services, and disable the repository again.

## Resource validation

The first post-install observation showed:

| Resource | Observed state |
|---|---|
| Guest memory | 7.8 GiB total, approximately 2.5 GiB used, 5.3 GiB available |
| Swap | 4.0 GiB configured, effectively unused |
| Root filesystem | 44 GiB total, 23 GiB used, 20 GiB available, 55% utilization |

These values are an initial baseline with no monitored endpoint agents. Capacity will be reviewed as event volume grows.

## Completed validation

- [x] Opened the dashboard from the trusted analyst laptop
- [x] Accepted the expected self-signed certificate warning locally
- [x] Authenticated as the Wazuh dashboard administrator
- [x] Confirmed dashboard health and the initial agent count
- [x] Protected the credential archive with root-only permissions
- [x] Disabled the Wazuh repository after installation
- [x] Applied pending Ubuntu package updates
- [x] Confirmed all four Wazuh services remained active
- [x] Enabled VM start at boot
- [x] Created the `wazuh-4147-installed` snapshot without VM RAM
