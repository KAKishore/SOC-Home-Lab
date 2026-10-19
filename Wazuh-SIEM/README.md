# Wazuh SIEM | SOC Home Lab

## Overview

This project documents my hands-on experience building a Wazuh-based SOC home lab to practice security monitoring, log analysis, threat hunting, and incident investigation.

My goal is to understand how security events are generated, collected, analyzed, and investigated in a SOC environment.

## Lab Environment

| Component | Purpose |
|---|---|
| VirtualBox | Virtualization platform |
| Ubuntu Server 24.04 LTS | Wazuh server |
| Wazuh 4.14.8 (rc2) | Centralized security monitoring and analysis |
| Windows 11 VM | Monitored endpoint |
| Wazuh Agent | Endpoint monitoring and log collection |


## Architecture

The SOC home lab runs in VirtualBox, using NAT and Host-only networking for communication between the Ubuntu-based Wazuh server and the Windows 11 endpoint.

Wazuh provides centralized security monitoring, while Windows and Linux security events are analyzed through the Wazuh Dashboard.

The architecture diagram, network configuration, and setup details are documented in [Part 1 — Lab Setup & Architecture](part-1-wazuh-lab-setup/README.md).


## Project Progress

| Phase | Description | Status |
|---|---|---|
| 1 | Lab Setup and Architecture | Completed |
| 2 | Security Event Analysis, Threat Hunting & MITRE ATT&CK | Completed |
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

- [Part 1 — Lab Setup & Architecture](part-1-wazuh-lab-setup/README.md)
- [Part 2 — Security Investigations](part-2-security-investigations/README.md)

Each section includes technical documentation, investigation findings, screenshots, and supporting evidence.

All security testing was performed in an authorized home lab environment.

