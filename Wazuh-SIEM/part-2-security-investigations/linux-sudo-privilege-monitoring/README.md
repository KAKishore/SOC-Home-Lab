
# Linux Sudo Privilege Monitoring

## 1. Investigation Objective

Investigate Linux privilege-related activity using Wazuh SIEM to identify and analyze commands executed through `sudo`.

## 2. Lab Environment

- SIEM: Wazuh 4.14.8
- Operating System: Ubuntu 24.04
- Monitored Endpoint: wazuh-server
- Log Source: Linux authentication logs
- Detection Rule: 5402

## 3. Investigation Scenario

An authorized user executed a command using `sudo` in the controlled SOC lab environment.

The objective was to examine how Wazuh detects and records privileged activity.

## 4. Detection and Findings

| Attribute | Observation |
|---|---|
| Wazuh Rule ID | 5402 |
| Alert Level | 3 |
| User | amita |
| Privileged Account | root |
| Activity | Sudo command execution |
| Endpoint | wazuh-server |

## 5. SOC Analyst Investigation

The alert was reviewed to understand:

- Which user initiated the privileged action
- Whether the command was executed through `sudo`
- Which privileged account was involved
- Whether the activity was expected or suspicious

The observed activity was authorized and performed as part of controlled lab testing.

### Assessment

**Classification:** Expected administrative activity

**Disposition:** Benign / Authorized

Although the activity was legitimate, monitoring sudo execution provides useful visibility into privileged actions that may require investigation.

## 6. Evidence

### Wazuh JSON Alert Evidence

- [Linux Sudo Privilege Activity — Rule 5402](evidence/linux-sudo-privilege-5402.json)

## 7. Key Learning Outcomes

- Identified privileged Linux activity using Wazuh
- Analyzed Rule 5402
- Distinguished authorized administrative actions from potentially suspicious behavior
- Practiced documenting SOC investigation findings

## 8. Conclusion

Wazuh successfully detected authorized sudo activity on the monitored Linux system.

This investigation demonstrates how SIEM monitoring supports visibility into privileged account activity and helps analysts assess administrative actions.
