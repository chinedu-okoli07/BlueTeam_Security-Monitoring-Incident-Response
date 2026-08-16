# 🛡️ Project 04 — Blue Team: Security Monitoring & Incident Response

> **Somewhere in the noise, an attacker left a trace. Find it.**

![Blue Team](https://img.shields.io/badge/Project-Blue%20Team-blue)
![Security Monitoring](https://img.shields.io/badge/Focus-Security%20Monitoring-orange)
![Incident Response](https://img.shields.io/badge/Focus-Incident%20Response-red)
![Linux](https://img.shields.io/badge/Platform-Linux-black)

## 📌 Project Overview

This project focuses on **Security Monitoring and Incident Response** from a Blue Team / SOC perspective.

The investigation was conducted using provided Linux authentication and system logs:

- `auth.log`
- `syslog.log`

The objective was to identify suspicious activity, analyze related events, develop detection logic, classify incidents by severity, and recommend appropriate response actions.

---

## 🎯 Objectives

The investigation aimed to:

- Analyze authentication and system logs
- Identify failed and successful authentication attempts
- Identify suspicious source IP addresses
- Detect unusual user and system activity
- Investigate privileged operations
- Identify account-management activity
- Analyze scheduled-task activity
- Develop security detection rules
- Classify suspicious activity by severity
- Recommend incident response actions
- Develop a structured incident response workflow
- Provide security recommendations

---

## 🔍 Investigation Summary

The log analysis identified several suspicious activities occurring within the broader investigation timeline.

### Key findings

| Finding | Observation | Initial Assessment |
|---|---|---|
| Repeated authentication failures | Multiple `Failed password` events targeting different accounts | Suspicious |
| Common source IP | Multiple authentication attempts associated with `198.51.100.23` | Possible credential-guessing activity |
| Successful authentication | `backup` account successfully authenticated after repeated failures | **High** |
| Privileged activity | `sudo` and `root` activity observed | **High** |
| Account activity | New user/group activity involving `sysupdate` | **High** |
| Password changes | Account password modification activity observed | Suspicious |
| Cron activity | Scheduled-task activity within the investigation timeline | **High** |
| System activity | `systemd-logind` session activity used to establish timeline | Investigative evidence |

---

## 🚨 Incident Timeline

The investigation showed a sequence of events that required correlation rather than treating each log entry independently:

```text
Repeated Failed Authentication
            ↓
Multiple Accounts Targeted
            ↓
Successful Authentication
            ↓
Privileged / Root Activity
            ↓
Account Creation / Modification
            ↓
Scheduled Task / Cron Activity
            ↓
Potential Persistence
