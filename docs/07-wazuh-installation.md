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

## Credential handling

The assistant generated the dashboard administrator password and a credential archive containing certificates, cluster keys, and service passwords.

Public-repository rules:

- Never commit `wazuh-install-files.tar`.
- Never publish the generated administrator password.
- Never publish screenshots containing passwords or tokens.
- Keep the credentials in a password manager.
- Keep the on-server credential archive readable only by root.

## Validation still pending

- [ ] Open the dashboard from the trusted analyst laptop
- [ ] Accept the expected self-signed certificate warning
- [ ] Authenticate as the Wazuh dashboard administrator
- [ ] Confirm dashboard health and initial agent count
- [ ] Protect the credential archive permissions
- [ ] Apply the documented Wazuh repository update policy
- [ ] Create a post-installation snapshot
