# Wazuh installation record

## Deployment summary

| Item | As-built value |
|---|---|
| Deployment type | All-in-one |
| Wazuh version | 4.14.7 |
| Operating system | Ubuntu Server 24.04 LTS |
| Installation method | Official Wazuh installation assistant |
| Dashboard access | HTTPS from the trusted management network |
| Credential storage | Private; excluded from GitHub |

The manager, indexer, dashboard, and Filebeat run together on one VM. This layout is appropriate for the small educational environment and reduces resource overhead.

## Installation and validation

The official all-in-one installation workflow completed successfully. The following milestones were observed:

- Prerequisite and resource checks passed.
- Certificates and service credentials were generated locally.
- The indexer was installed and initialized.
- The manager, Filebeat, and dashboard were configured.
- The installer reported successful completion.

All four central services were validated as active after installation, operating-system maintenance, and later routine credential maintenance.

## Dashboard validation

- The dashboard loaded over HTTPS from the trusted analyst laptop.
- The expected locally issued certificate warning was handled on the management device.
- Administrator authentication succeeded.
- The first Windows endpoint was later enrolled and confirmed active.
- No dashboard credential or private network address is included in public documentation.

## Credential controls

- Generated credential material is restricted to the system administrator.
- Dashboard credentials are stored outside source control.
- Raw screenshots containing credentials or tokens are not published.
- Routine credential maintenance was followed by service-health and authentication checks.
- Dashboard authentication must be revalidated after restoring an older recovery point.

## Update policy

The Wazuh package source is disabled during normal operation to prevent an unplanned independent upgrade of tightly coupled components. Future upgrades will follow a deliberate process: create a recovery point, review compatibility guidance, update compatible components together, validate services, and return the repository to its normal disabled state.

## Capacity observation

Initial measurements showed sufficient headroom for the Wazuh platform and one monitored endpoint. Capacity will be reviewed as telemetry volume grows and before any additional guest is deployed.

## Completed validation

- [x] Opened the dashboard from the trusted analyst laptop
- [x] Authenticated as the dashboard administrator
- [x] Protected locally generated credential material
- [x] Applied operating-system maintenance
- [x] Confirmed all four central services remained active
- [x] Enabled VM start at boot
- [x] Created recovery points
- [x] Revalidated authentication after credential maintenance

