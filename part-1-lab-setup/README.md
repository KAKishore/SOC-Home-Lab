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

