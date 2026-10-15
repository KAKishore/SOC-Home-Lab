# Wazuh SIEM | SOC Home Lab

## Overview

This project documents my hands-on experience building a Wazuh-based SOC home lab to practice security monitoring, log analysis, threat hunting, and incident investigation.

My goal is to understand how security events are generated, collected, analyzed, and investigated in a SOC environment.

## Lab Environment

| Component | Purpose |
|---|---|
| VirtualBox | Virtualization platform |
| Ubuntu Server 24.04 LTS | Wazuh server |
| Wazuh 4.14.8 | Centralized security monitoring and analysis |
| Windows 11 VM | Monitored endpoint |
| Wazuh Agent | Endpoint monitoring and log collection |

## Architecture

The lab uses VirtualBox with NAT and Host-only networking to establish communication between the Windows 11 endpoint and the Ubuntu-based Wazuh server.

The Wazuh Agent installed on Windows 11 collects endpoint security information and forwards it to the Wazuh server for centralized monitoring and analysis.

An architecture diagram will be added to the detailed setup documentation.

## Project Progress

| Phase | Description | Status |
|---|---|---|
| 1 | Lab Setup and Architecture | Completed |
| 2 | Security Event Analysis, Threat Hunting & MITRE ATT&CK | In Progress |
| 3 | Sysmon Integration & Endpoint Detection | Planned |
| 4 | Network Monitoring & Lab Expansion | Planned |
| 5 | Advanced Detection & Incident Investigation | Planned |

## Initial Results

- Successfully deployed Wazuh on Ubuntu Server.
- Configured network connectivity between the Windows 11 endpoint and Wazuh server.
- Installed and connected the Wazuh Agent on Windows 11.
- Verified the endpoint's active status in the Wazuh Dashboard.
- Confirmed that endpoint security alerts are being collected and displayed.

## Documentation

Detailed setup procedures, troubleshooting, validation results, and investigation findings will be documented in separate sections as the project progresses.

All security testing is performed within my authorized home lab environment.
