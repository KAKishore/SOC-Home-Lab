# Part 1 — SOC Lab Setup & Architecture

## 1. Objective

The objective of this project is to build a functional SOC home lab to practice security monitoring, log collection, threat detection, and incident investigation.

Part 1 focuses on setting up the virtual environment, configuring network connectivity, and establishing centralized log collection.

## 2. Lab Environment

| Component | Deployment | Purpose |
|---|---|---|
| VirtualBox | Physical host | Virtualization |
| Splunk Enterprise | Physical host | SIEM and log analysis |
| pfSense CE | Virtual machine | Firewall, routing, and DHCP |
| Windows 11 | Virtual machine | Monitored endpoint |
| Kali Linux | Virtual machine | Controlled security testing |
| Sysmon | Windows 11 VM | Endpoint telemetry |
| Splunk Universal Forwarder | Windows 11 VM | Log forwarding |
| Wazuh | Planned | Security monitoring and detection |

## 3. Network Architecture & pfSense Configuration

I configured an isolated virtual network using VirtualBox Internal Network and pfSense CE to manage routing and connectivity between the lab environment and the physical host.

### Network Configuration

| Component | Configuration |
|---|---|
| Internal network | `SOC-LAN` |
| Lab subnet | `10.10.10.0/24` |
| pfSense WAN | VirtualBox NAT |
| pfSense LAN | `10.10.10.1/24` |
| DHCP range | `10.10.10.100–10.10.10.199` |
| Windows 11 VM | `10.10.10.100` |
| Splunk Enterprise | Physical host, TCP `9997` |

### VirtualBox Network Adapters

- **pfSense Adapter 1:** NAT (WAN)
- **pfSense Adapter 2:** Internal Network — `SOC-LAN` (LAN)
- **Windows 11:** Internal Network — `SOC-LAN`
- **Kali Linux:** Internal Network — `SOC-LAN`

### Network Troubleshooting

Initially, I configured the lab using the `192.168.1.0/24` subnet, which overlapped with my physical network.

This caused connectivity issues when the Windows 11 VM attempted to communicate with Splunk Enterprise on the physical host.

To resolve the issue, I changed the pfSense LAN network to `10.10.10.0/24`, updated the DHCP configuration, and verified connectivity from the Windows endpoint to the Splunk receiving port.

The connectivity test confirmed that TCP port `9997` was reachable.

### Validation

The updated network configuration allowed the Windows endpoint to communicate with Splunk Enterprise through the pfSense gateway.

This established the network connectivity required for centralized log forwarding.

## 4. Endpoint Monitoring & Splunk Log Collection

### Sysmon Configuration

I installed Microsoft Sysmon on the Windows 11 virtual machine to collect detailed endpoint activity.

Sysmon records events in the following Windows Event Log channel:

`Microsoft-Windows-Sysmon/Operational`

This provides endpoint telemetry that can be used for process monitoring and future security investigations.

### Splunk Enterprise

I installed Splunk Enterprise on the physical Windows host to serve as the centralized SIEM platform.

I configured Splunk to receive forwarded events on TCP port `9997`.

### Splunk Universal Forwarder

I installed Splunk Universal Forwarder on the Windows 11 VM to forward Sysmon events to Splunk Enterprise.

I configured the following file:

`C:\Program Files\SplunkUniversalForwarder\etc\system\local\inputs.conf`

Configuration:

```ini
[WinEventLog://Microsoft-Windows-Sysmon/Operational]
disabled = 0
```

The forwarder was configured to send events to the Splunk receiver on the physical host.

### Troubleshooting Log Collection

During configuration, the Splunk Universal Forwarder established an active connection with Splunk Enterprise, but Sysmon events were not appearing in search results.

I investigated the forwarder configuration and encountered two issues:

1. The input configuration file was initially named incorrectly. I corrected it to `inputs.conf`.
2. The forwarder encountered an access-denied error when reading the Sysmon Operational event log.

To resolve the permission issue, I added the Splunk Universal Forwarder service identity to the Windows Event Log Readers group using an elevated command prompt:

```cmd
net localgroup "Event Log Readers" "NT SERVICE\SplunkForwarder" /add
```

After restarting the Splunk Universal Forwarder service, Sysmon events were successfully forwarded.

### Validation

I verified that the forwarder connection was active and that Sysmon events were searchable in Splunk Enterprise.

Example SPL search:

```spl
index=* host="SOC-WIN11" source="WinEventLog:Microsoft-Windows-Sysmon/Operational"
```

The successful ingestion confirmed that the endpoint-to-SIEM log collection pipeline was functioning.

This completed the initial centralized endpoint monitoring configuration.

