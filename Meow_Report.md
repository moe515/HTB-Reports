# Hack The Box Security Report — Meow

## Executive Summary

The Meow lab demonstrated how an exposed Telnet service with no effective authentication can provide direct privileged access to a Linux host. Enumeration identified Telnet on TCP port 23, and validation in the authorized Hack The Box environment confirmed that the root account could be accessed without a password.

**Risk rating:** Critical  
**Primary weakness:** Unauthenticated privileged Telnet access  
**Outcome:** Root-level access was obtained in the lab

> This report documents activity performed only in an authorized Hack The Box training environment. The captured flag is intentionally omitted.

## Scope

- **Machine:** Meow
- **Platform:** Hack The Box Starting Point
- **Difficulty:** Very Easy
- **Operating system:** Linux
- **Service assessed:** Telnet
- **Authorization:** HTB lab environment

## Enumeration

An Nmap scan with default scripts and service-version detection was performed:

```bash
nmap -sC -sV -oA meow-scan <TARGET_IP>
```

### Key Result

| Port | Protocol | Service | Observation |
|---|---|---|---|
| 23 | TCP | Telnet | Remote login service was accessible |

## Finding: Unauthenticated Root Access

### Description

The Telnet service allowed direct authentication as the root user without a password. Telnet also transmits session data without encryption, making it unsuitable for secure remote administration.

### Validation

Within the authorized lab, a Telnet connection was established:

```bash
telnet <TARGET_IP>
```

The service provided a root shell without requiring a password.

### Impact

An attacker who could reach the service could obtain complete control of the host, including the ability to read or modify data, install software, disable security controls, and establish persistence.

### Evidence

- TCP port 23 exposed a Telnet service.
- The root account was accessible without a password.
- A privileged shell was obtained.
- The training objective was completed; the flag value is intentionally omitted.

## Remediation

1. Disable Telnet and replace it with SSH.
2. Prohibit remote root login.
3. Require unique, strong credentials and key-based authentication.
4. Restrict administrative services with firewalls, network segmentation, or a VPN.
5. Monitor remote-login activity and privileged account usage.
6. Remove unused services and apply secure baseline configurations.

## Defensive Detection Notes

A SOC team should investigate:

- Connections to TCP port 23
- Remote logins using privileged accounts
- New sessions from unfamiliar source addresses
- Unexpected commands or configuration changes after a remote login
- Telnet traffic observed anywhere in a modern production environment

## Tools Used

- Nmap
- Telnet client
- Linux command-line utilities

## Lessons Learned

This lab showed how basic service enumeration can reveal a critical authentication failure. Secure remote administration requires encrypted protocols, strong authentication, limited privilege, and restricted network exposure.
