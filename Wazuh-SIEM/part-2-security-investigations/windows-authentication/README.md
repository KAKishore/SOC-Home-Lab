# Windows Authentication Investigation — Wazuh SIEM

## 1. Investigation Objective

Analyze Windows authentication events collected by Wazuh SIEM to identify failed logins, successful logins, and special privileges assigned during authentication.

All activities were performed in an authorized SOC home lab environment.

## 2. Investigation Environment

| Component | Details |
|---|---|
| Endpoint | Windows 11 VM (`SOC-WIN11`) |
| User Account | `SOCAnalyst` |
| Wazuh Agent | `001` |
| SIEM | Wazuh 4.14.8 |
| Log Source | Windows Security Event Log |
| Investigation Date | October 15, 2026 |

## 3. Security Events Analyzed

| Event ID | Wazuh Rule | Level | Description |
|---|---|---|---|
| 4625 | 60122 | 5 | Failed authentication |
| 4624 | 60118 | 3 | Successful authentication |
| 4672 | 67028 | 3 | Special privileges assigned to a new logon |

## 4. Investigation Findings

### Event 4625 — Failed Authentication

- Account: `SOCAnalyst`
- Logon Type: `2` (Interactive)
- Source IP: `127.0.0.1`
- Failure Substatus: `0xC000006A` (Incorrect password)
- Event Time: `09:46:52 UTC`
- Wazuh Rule: `60122`

Wazuh successfully detected the failed login and generated a Level 5 alert.

### Event 4624 — Successful Authentication

- Account: `SOCAnalyst`
- Logon Type: `2` (Interactive)
- Source IP: `127.0.0.1`
- Event Time: `09:47:39 UTC`
- Wazuh Rule: `60118`

A successful interactive login was recorded approximately 47 seconds after the failed attempt.

### Event 4672 — Special Privileges Assigned

- Account: `SOCAnalyst`
- Event Time: `09:47:39 UTC`
- Wazuh Rule: `67028`
- Assigned privileges included `SeDebugPrivilege`, `SeBackupPrivilege`, and `SeTakeOwnershipPrivilege`.

The Event 4672 Logon ID (`0xA8CCA7`) matched the Linked Logon ID in Event 4624, supporting correlation between the authentication and privilege-assignment events.

## 5. SOC Analysis

The event sequence showed:

1. A failed interactive login due to an incorrect password.
2. A successful interactive login for the same account.
3. Special privileges assigned in an associated logon session.

These events were consistent with controlled, authorized lab activity. No evidence established brute-force activity, unauthorized access, or malicious privilege escalation.

## 6. Evidence

Wazuh alert JSON exports:

- `failed-logon-4625.json`
- `successful-logon-4624.json`
- `privileged-logon-4672.json`

Screenshots and JSON evidence will be added to this investigation folder.

## 7. Conclusion

Wazuh successfully collected and classified Windows authentication events, enabling correlation of failed and successful logins with associated privilege-assignment activity.

This investigation demonstrated practical SOC skills in Windows event analysis, Wazuh rule interpretation, authentication monitoring, and evidence-based investigation.

---

[← Part 2 — Security Investigations Overview](../README.md)
