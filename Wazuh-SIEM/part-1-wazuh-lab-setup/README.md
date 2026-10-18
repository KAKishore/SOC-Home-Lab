# Part 1 — Wazuh SIEM Lab Setup & Architecture

## 1. Objective

The objective of this phase is to build a functional Wazuh-based SOC home lab for centralized security monitoring, log collection, threat hunting, and incident investigation.

Part 1 focuses on configuring the virtual environment, deploying Wazuh, establishing network connectivity, and connecting a Windows endpoint for security monitoring.

## 2. Lab Environment

| Component | Configuration | Purpose |
|---|---|---|
| VirtualBox | Windows physical host | Virtualization |
| Ubuntu Server | 24.04 LTS | Wazuh server operating system |
| Wazuh | 4.14.8, all-in-one deployment | SIEM and security monitoring |
| Windows 11 Pro | Virtual machine | Monitored endpoint |
| Wazuh Agent | 4.14.8 | Endpoint monitoring and log collection |

### Virtual Machine Resources

| Resource | Ubuntu Wazuh Server | Windows 11 Endpoint |
|---|---|---|
| Memory | 8 GB | 6 GB |
| vCPUs | 4 | 2 |
| Virtual disk | 100 GB | 80 GB |
| Network Adapter 1 | NAT | NAT |
| Network Adapter 2 | Host-only | Host-only |

## 3. Network Architecture

I configured two VirtualBox network adapters for each virtual machine:

- NAT provides outbound network connectivity.
- Host-only networking enables communication between the Windows endpoint, Wazuh server, and physical host.

### Network Configuration

| Component | IP Address |
|---|---|
| Ubuntu Wazuh Server | `192.168.56.101` |
| Windows 11 Endpoint | `192.168.56.102` |
| Host-only subnet | `192.168.56.0/24` |

The Ubuntu server uses the `enp0s8` interface for host-only connectivity.

### Connectivity Validation

I verified connectivity between the Windows 11 endpoint and the Ubuntu Wazuh server using ICMP ping.

Successful communication confirmed that the endpoint could reach the Wazuh server through the host-only network.

## 4. Wazuh Server Deployment

I installed Ubuntu Server 24.04 LTS in VirtualBox and deployed Wazuh 4.14.8 using an all-in-one configuration.

The deployment includes:

- Wazuh Manager — Receives and analyzes security events.
- Wazuh Indexer — Stores and indexes security data.
- Wazuh Dashboard — Provides a web interface for monitoring and investigation.

### Service Validation

After installation, I verified that the Wazuh Manager, Indexer, and Dashboard services were running.

I also confirmed that the Wazuh Indexer cluster was healthy and the Manager API was accessible.

### Dashboard Access

I configured SSH port forwarding to access the Wazuh Dashboard from the physical Windows host.

The following command was executed in Windows PowerShell:

```powershell
ssh -N -L 8443:127.0.0.1:443 -p 2222 amita@127.0.0.1
```

This command forwards local port `8443` on the Windows host through the SSH connection to port `443` on the Ubuntu Wazuh server.

I accessed the dashboard using:

`https://localhost:8443`

The SSH tunnel provided encrypted access to the Wazuh Dashboard without exposing its web service directly to the external network.

## 5. Windows 11 Endpoint Monitoring

I configured a Windows 11 Pro virtual machine as the monitored endpoint.

### Wazuh Agent Installation

I installed Wazuh Agent 4.14.8 on the Windows endpoint and configured it to communicate with the Wazuh Manager using the host-only network.

Wazuh Manager address:

`192.168.56.101`

### Agent Validation

I verified the following in the Wazuh Dashboard:

| Field | Result |
|---|---|
| Agent ID | `001` |
| Agent name | `Windows11-SOC-Endpoint` |
| Operating system | Windows 11 Pro |
| Agent version | 4.14.8 |
| Agent status | Active |

The active agent status confirmed successful communication between the Windows endpoint and the Wazuh server.

## 6. Initial Security Monitoring

After connecting the Windows endpoint, I explored the Wazuh Dashboard and Threat Hunting interface.

The dashboard displayed security events associated with the monitored endpoint, including security configuration assessment findings and Windows system events.

I reviewed the event list, including Wazuh rule IDs, descriptions, severity levels, and timestamps.

A detailed security investigation will be documented in Part 2.


## 7. Troubleshooting

During deployment, I resolved the following setup challenges:

| Challenge | Resolution |
|---|---|
| VM Performance | Verified Wazuh services after temporary Ubuntu VM performance issues. |
| Network Connectivity | Configured host-only networking to enable communication between both VMs. |
| Agent Installation | Resolved the installer file-location issue and successfully installed the Windows Wazuh Agent. |
| Dashboard Access | Configured SSH port forwarding to securely access the Wazuh Dashboard from the physical host. |


## 8. SOC Lab Architecture & Security Event Flow

The diagram illustrates the deployed Wazuh SIEM environment and how security events are collected, processed, and investigated.

<p align="center">
  <img src="Wazuh%20Home%20Lab%20Architecture%20Flow.png" alt="Wazuh SOC Lab Architecture" width="650">
</p>

### Security Event Flow

- **Windows 11:** The Wazuh Agent collects and forwards Windows security events.
- **Ubuntu Server:** Wazuh monitors local SSH, sudo, and file integrity activity.
- **Wazuh Manager:** Analyzes events using decoders and detection rules.
- **Filebeat & Indexer:** Forward and store alerts for searching.
- **Wazuh Dashboard:** Provides centralized alert review and investigation.

**Network:** NAT for outbound connectivity, host-only networking for VM communication, and an SSH tunnel for dashboard access.


## 9. Validation & Lessons Learned

### Validation
- Verified Wazuh Manager, Indexer, and Dashboard services.
- Confirmed network connectivity between both VMs.
- Connected the Windows 11 Wazuh Agent (ID 001).
- Verified security events in Wazuh Threat Hunting.
- Successfully accessed the Dashboard through an SSH tunnel.

### Lessons Learned
- Configuring virtual networks and troubleshooting connectivity.
- Deploying and validating Wazuh SIEM components.
- Understanding endpoint log collection and alert processing.
- Distinguishing agent connectivity from successful log ingestion.


## 10. Next Steps

Part 2 documents hands-on security investigations involving Windows authentication, Linux SSH activity, sudo privilege usage, and file integrity monitoring (FIM), including Wazuh alert analysis and MITRE ATT&CK mappings.

All security testing is performed within my authorized home lab environment.
