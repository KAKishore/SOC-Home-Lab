
# Part 2 — Wazuh SIEM Security Investigations Overview

## 1. Objective

Investigate security events collected from Windows and Linux systems using Wazuh SIEM, focusing on event analysis, detection rules, and evidence-based investigation.

All activities were performed in an authorized home lab environment.

## 2. Investigation Environment

| Component | Purpose |
|---|---|
| Windows 11 VM | Windows authentication event analysis |
| Ubuntu Server 24.04 | Linux authentication, sudo, and FIM monitoring |
| Wazuh 4.14.8 | Centralized detection and investigation |
| Wazuh Threat Hunting | Alert review and event analysis |

The environment and network configuration are documented in [Part 1 — Lab Setup & Architecture](../part-1-wazuh-lab-setup/README.md).


## 3. Completed Investigations

| Investigation | Events / Wazuh Rules | Status |
|---|---|---|
| [Windows Authentication](windows-authentication/README.md) | 4625, 4624, 4672 | Completed |
| [Linux SSH Authentication](linux-ssh-authentication/README.md) | 5760, 5715 | Completed |
| [Linux Sudo Privilege Monitoring](linux-sudo-privilege-monitoring/README.md) | 5402 | Completed |
| [Linux File Integrity Monitoring](linux-file-integrity-monitoring/README.md) | 554, 550, 553 | Completed |


## 4. Investigation Methodology

1. Generate or identify security activity in the lab.
2. Review the corresponding source logs.
3. Identify Wazuh alerts and detection rules.
4. Analyze timestamps, accounts, event details, and severity.
5. Review relevant MITRE ATT&CK mappings.
6. Document evidence, findings, and conclusions.

## 5. Investigation Documentation

Each investigation includes a dedicated report documenting the investigation objective, lab environment, detection findings, SOC analysis, and conclusions.

Supporting evidence is organized within each investigation's `evidence/` directory, including Wazuh dashboard screenshots and JSON alert exports.


## 6. Key Learning Outcomes

- Analyzed Windows and Linux security events.
- Correlated source logs with Wazuh alerts.
- Distinguished authorized activity from suspicious behavior.
- Investigated authentication, privilege usage, and file changes.
- Practiced evidence-based SOC investigation and documentation.

---

[← Part 1 — Wazuh Lab Setup & Architecture](../part-1-wazuh-lab-setup/README.md)
