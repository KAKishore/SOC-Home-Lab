# Linux SSH Authentication Investigation — Wazuh SIEM

## 1. Investigation Objective

Investigate failed and successful SSH authentication events on an Ubuntu Linux server using Wazuh SIEM.

The investigation focuses on authentication monitoring, Wazuh detection rules, event correlation, and identifying potential security concerns.

All activities were performed in an authorized SOC home lab environment.

## 2. Investigation Environment

| Component | Details |
|---|---|
| Operating System | Ubuntu Server 24.04 |
| Hostname | `wazuh-server` |
| User Account | `amita` |
| SIEM | Wazuh 4.14.8 |
| Log Sources | SSH authentication logs and systemd journal |
| Monitoring | Local Wazuh Manager |
| Investigation Date | October 14–15, 2026 |

## 3. Security Events Analyzed

| Activity | Wazuh Rule | Level | Description |
|---|---|---|---|
| Failed SSH Authentication | 5760 | 5 | SSH authentication failed |
| Successful SSH Authentication | 5715 | 3 | SSH authentication succeeded |

## 4. Investigation Findings

### Failed SSH Authentication — Rule 5760

A controlled failed SSH login was detected by Wazuh.

- Account: `amita`
- Source IP: `10.0.2.2`
- Source Port: `62765`
- SSH Process: `sshd[11073]`
- Event Time: October 15, 2026, `14:16:00 UTC`
- Wazuh Alert Time: `14:16:01.521 UTC`
- Severity: Level 5
- MITRE ATT&CK Mapping: `T1110.001` — Password Guessing

Wazuh generated an alert identifying the failed authentication attempt.

### Successful SSH Authentication — Rule 5715

A successful SSH login was also recorded.

- Account: `amita`
- Source IP: `10.0.2.2`
- Source Port: `57167`
- Event Time: October 14, 2026, `19:12:05 UTC`
- Severity: Level 3
- MITRE ATT&CK Mappings: `T1078` — Valid Accounts; `T1021` — Remote Services

This event confirmed that Wazuh was collecting successful SSH authentication activity.

### Monitoring Coverage Observation

An earlier failed SSH authentication event occurred on October 14 at approximately `05:08 UTC`, before the Wazuh Manager and its log collector started around `05:22 UTC`.

The failed event was visible in the Linux source logs but had no corresponding Wazuh alert.

The event was subsequently tested using `wazuh-logtest`, which matched Rule `5760`.

This highlighted the importance of monitoring availability and distinguishing source-log evidence from events actually detected by the SIEM.

## 5. SOC Analysis

The investigation demonstrated that Wazuh detected both failed and successful SSH authentication activity.

The observed SSH connections originated from `10.0.2.2`, the VirtualBox NAT gateway used in this lab.

The reviewed events were consistent with authorized testing and administration. The evidence did not establish a brute-force attack or unauthorized access.

The investigation also identified a visibility limitation when authentication activity occurred before Wazuh monitoring became available.

## 6. Evidence

### Wazuh SSH Authentication Alerts

- Failed SSH Authentication — Rule `5760`
- Successful SSH Authentication — Rule `5715`

Supporting JSON alert records and screenshots will be linked here after uploading them to the investigation evidence folder.

## 7. Key Learning Outcomes

- Investigated Linux SSH authentication events.
- Reviewed SSH source logs and Wazuh alerts.
- Analyzed authentication timestamps, accounts, and source IP addresses.
- Interpreted Wazuh detection rules and MITRE ATT&CK mappings.
- Identified a monitoring coverage gap during service startup.

## 8. Conclusion

Wazuh successfully detected and classified SSH authentication activity during the monitored testing period.

The investigation strengthened practical SOC skills in Linux log analysis, SSH authentication monitoring, SIEM alert validation, and evidence-based investigation.

---

[← Part 2 — Security Investigations Overview](../README.md)
