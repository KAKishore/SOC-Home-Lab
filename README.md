# SOC Home Lab | SIEM Monitoring & Incident Investigation

## Overview

This repository documents my hands-on Security Operations Center (SOC) home lab projects, focusing on SIEM monitoring, endpoint security, log analysis, threat detection, and incident investigation.

The repository includes Wazuh and Splunk lab environments, with completed investigations, technical documentation, and supporting evidence.

## SOC Lab Environments

### Wazuh SIEM Lab — Completed

- VirtualBox
- Ubuntu Server 24.04
- Wazuh 4.14.8 (rc2)
- Windows 11 VM
- Wazuh Agents

### Splunk SIEM Lab — Separate Project

- Splunk Enterprise
- Sysmon
- Kali Linux
- Windows endpoint

Network monitoring and additional integrations are planned.


## Architecture

This repository contains separate Wazuh and Splunk SIEM lab environments.

The Wazuh lab uses VirtualBox, Ubuntu Server, and a Windows 11 endpoint for centralized security monitoring and investigation.

[View Wazuh Lab Architecture](Wazuh-SIEM/part-1-wazuh-lab-setup/README.md)

The Splunk lab is maintained as a separate project.


## Project Progress

| Project | Status |
|---|---|
| Wazuh Lab Setup & Architecture | Completed |
| Wazuh Security Investigations (4) | Completed |
| Splunk SIEM Lab | In Progress |
| Sysmon Integration with Wazuh | Planned |
| Network Monitoring & Advanced Detection | Planned |


## Current Results

- Deployed Wazuh 4.14.8 on Ubuntu Server.
- Connected and monitored a Windows 11 endpoint.
- Completed four Wazuh security investigations.
- Analyzed Windows authentication, Linux SSH, sudo, and FIM alerts.
- Documented findings with JSON evidence and screenshots.
- Started a separate Splunk SIEM lab project.



## Documentation

- [Wazuh SIEM — Project Overview](Wazuh-SIEM/README.md)
- [Part 1 — Wazuh Lab Setup & Architecture](Wazuh-SIEM/part-1-wazuh-lab-setup/README.md)
- [Part 2 — Security Investigations](Wazuh-SIEM/part-2-security-investigations/README.md)
- [Splunk SIEM Lab](Splunk-SIEM/)

All security testing was performed in an authorized home lab environment.

