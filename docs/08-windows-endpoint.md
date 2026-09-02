# Windows endpoint build record

## Deployment status

The first monitored Windows endpoint is operational. It runs Windows 11 Enterprise Evaluation, reports to Wazuh under the sanitized alias `ENDPOINT-001`, and automatically starts both Wazuh Agent and Sysmon.

## Virtualization design

The endpoint uses a resource-conscious configuration suitable for the single-host lab:

- UEFI firmware with Windows 11 security prerequisites
- Paravirtualized storage and networking
- Fixed guest memory to keep behavior predictable
- Guest-agent integration for clean hypervisor operations
- Proxmox firewall protection on the virtual network interface

Exact VM identifiers, resource allocations, device paths, and private network details are intentionally excluded from the public record.

## Operating-system preparation

- Installed Windows 11 Enterprise Evaluation 25H2 x64 from an official image.
- Used a dedicated local administrative account; its identifier and password are not documented.
- Installed the required paravirtualized drivers.
- Enabled guest-agent support.
- Applied Windows, Defender, .NET, and platform updates until Windows Update reported the system up to date.
- Confirmed network connectivity before endpoint enrollment.
- Created recovery points after the clean update stage and after agent enrollment.

## Wazuh Agent

Wazuh Agent 4.14.7 was installed and enrolled successfully. The endpoint appears as active in the dashboard, and the Windows service is `Running` with an `Automatic` startup type.

Manager addressing, agent identifiers, enrollment material, and endpoint addressing are intentionally omitted.

## Sysmon deployment

Sysmon 15.21 was installed from Microsoft Sysinternals with the SwiftOnSecurity community configuration as a starting baseline.

Validated state:

- The Sysmon service is running and starts automatically.
- The community configuration loaded successfully.
- Wazuh Agent collects the Microsoft Sysmon Operational event channel.
- Process creation, network connection, process termination, registry, and DNS-related event types were observed locally.
- A process-creation event successfully triggered a custom Wazuh detection.

## Naming observation

During the first investigation, telemetry showed that the Windows computer name did not yet match the public endpoint alias. The generated name is omitted. Name normalization and post-reboot agent validation remain tracked actions.

## Publication controls

- No Windows, Wazuh, or Linux credential is stored in the repository.
- Private addresses, host-generated identifiers, device paths, and raw JSON are omitted.
- Screenshots are not published until sensitive fields are cropped or redacted.
- The evaluation operating system is used only for the local educational lab.

