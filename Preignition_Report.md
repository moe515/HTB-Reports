# Hack The Box Security Report — Preignition

## Executive Summary

The Preignition lab demonstrated how hidden administrative pages and unchanged default credentials can expose a web application to unauthorized access. Enumeration identified an Nginx web service on TCP port 80, content discovery revealed an administrative login page, and validation in the authorized Hack The Box environment confirmed that default administrator credentials were still active.

**Risk rating:** High  
**Primary weaknesses:** Discoverable administrative interface and unchanged default credentials  
**Outcome:** Unauthorized access to the administrative panel was obtained in the lab

> This report documents activity performed only in an authorized Hack The Box training environment. The captured flag is intentionally omitted.

## Scope

- **Machine:** Preignition
- **Platform:** Hack The Box Starting Point
- **Difficulty:** Very Easy
- **Services assessed:** HTTP and web application
- **Authorization:** HTB lab environment

## Enumeration

A full TCP port scan with service-version detection was performed:

```bash
nmap -sV -Pn -p- -oA preignition-scan <TARGET_IP>
```

### Key Result

| Port | Protocol | Service | Observation |
|---|---|---|---|
| 80 | TCP | HTTP / Nginx 1.14.2 | Web application was accessible |

The exposed HTTP service became the primary target for further web-content discovery.

## Web Content Discovery

Gobuster was used with a common web-content wordlist and the `.php` extension:

```bash
gobuster dir -u http://<TARGET_IP> -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt -x .php
```

The scan discovered:

| Resource | HTTP status | Significance |
|---|---|---|
| `/admin.php` | 200 OK | Exposed administrative login page |

Finding the page did not itself provide access, but it revealed a sensitive authentication interface that required validation.

## Finding: Default Administrative Credentials

### Description

The administrative login page accepted unchanged default credentials. Default credentials are widely known and frequently tested by attackers, so leaving them active can allow unauthorized users to access privileged application functions.

### Validation

Within the authorized lab, the administrator account was tested with the product's default username and password. Authentication succeeded and provided access to the administrative panel.

The credential values and captured flag are intentionally omitted from this portfolio report.

### Impact

An attacker who discovers the administrative interface could gain privileged access without exploiting a software vulnerability. Depending on the application's functions, possible consequences include:

- Viewing or modifying protected information
- Changing application settings
- Creating or altering user accounts
- Uploading malicious content
- Establishing persistence
- Using administrative access to support further compromise

### Evidence

- TCP port 80 exposed an Nginx web service.
- Content discovery returned `/admin.php` with HTTP status 200.
- The administrative interface accepted unchanged default credentials.
- The training objective was completed; the flag value is intentionally omitted.

## Remediation

1. Change all vendor or default credentials before deploying an application.
2. Require long, unique passwords and multi-factor authentication for administrative accounts.
3. Restrict administrative interfaces to trusted networks, a VPN, or an allowlist.
4. Apply rate limiting and account lockout controls to authentication endpoints.
5. Avoid relying on hidden URLs as a security control.
6. Monitor authentication logs for repeated failures and unusual administrative logins.
7. Keep the web server and application patched and securely configured.

## Defensive Detection Notes

A SOC team should investigate:

- Requests to administrative paths from unfamiliar source addresses
- Repeated login attempts against `/admin.php`
- Successful administrative logins following multiple failures
- Administrative access from unusual locations or outside approved hours
- Configuration or account changes shortly after a new login
- Web requests using automated content-discovery patterns

## Tools Used

- Nmap
- Gobuster
- SecLists
- Web browser
- Linux command-line utilities

## Lessons Learned

This lab showed that directory discovery can expose sensitive interfaces, but the main security failure was weak credential management. Administrative pages should be protected by strong authentication, restricted network access, and continuous monitoring rather than secrecy alone.
