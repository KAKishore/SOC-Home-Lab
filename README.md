# SOC Home Lab | SIEM Monitoring & Incident Investigation

## Overview
This project documents my hands-on SOC home lab, built to practice security monitoring, log collection, threat detection, and incident investigation.

My goal is to understand how security events are generated, collected, and analyzed in a SOC environment.

## Lab Environment

| Tool | Purpose |
|---|---|
| VirtualBox | Virtualization |
| pfSense CE | Firewall and network routing |
| Windows 11 | Monitored endpoint |
| Kali Linux | Controlled security testing |
| Sysmon | Endpoint telemetry |
| Splunk Universal Forwarder | Log forwarding |
| Splunk Enterprise | SIEM and log analysis |
| Wazuh (Planned) | Security monitoring, endpoint detection, and log analysis |

## Architecture
The lab uses an isolated VirtualBox internal network (`SOC-LAN`) with pfSense as the gateway.

Windows 11 generates Sysmon events, which are forwarded to Splunk Enterprise running on the physical host.

*Architecture diagram coming soon.*

## Project Progress

| Part | Description | Status |
|---|---|---|
| 1 | SOC Lab Setup & Architecture | Completed |
| 2 | Endpoint Log Analysis | Planned |
| 3 | Wazuh Deployment & Monitoring | Planned |
| 4 | Attack Simulation & Detection | Planned |
| 5 | Incident Investigation & Reporting | Planned |

## Current Results
- Configured pfSense and an isolated lab network.
- Installed and configured Sysmon and Splunk Universal Forwarder.
- Successfully forwarded Sysmon events to Splunk Enterprise.
- Troubleshot networking and log collection issues.

## Documentation

- [Part 1 — SOC Lab Setup & Architecture](part-1-lab-setup/README.md)

---

*All security testing is intended for my authorized home lab environment.*
