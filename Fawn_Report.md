# Hack The Box Security Report — Fawn

## Executive Summary

The Fawn lab demonstrated the risk of exposing an FTP service that permits anonymous authentication and access to stored files. Enumeration identified FTP on TCP port 21, and validation in the authorized Hack The Box environment confirmed that an anonymous user could log in and retrieve data.

**Risk rating:** High  
**Primary weakness:** Anonymous FTP access to sensitive files  
**Outcome:** Unauthorized file access was obtained in the lab

> This report documents activity performed only in an authorized Hack The Box training environment. The captured flag is intentionally omitted.

## Scope

- **Machine:** Fawn
- **Platform:** Hack The Box Starting Point
- **Difficulty:** Very Easy
- **Operating system:** Linux
- **Service assessed:** FTP
- **Authorization:** HTB lab environment

## Enumeration

An Nmap scan with default scripts and service-version detection was performed:

```bash
nmap -sC -sV -oA fawn-scan <TARGET_IP>
```

### Key Result

| Port | Protocol | Service | Observation |
|---|---|---|---|
| 21 | TCP | FTP | Anonymous authentication was enabled |

## Finding: Anonymous FTP File Access

### Description

The FTP server allowed users to authenticate anonymously and access files without an individual account. FTP also transmits credentials and data without encryption, increasing the risk of interception.

### Validation

Within the authorized lab, the FTP service was accessed with an anonymous account:

```bash
ftp <TARGET_IP>
```

Directory contents were listed and a file was retrieved using standard FTP commands. The credential details and captured flag are intentionally omitted.

### Impact

An unauthenticated user could access exposed files. Depending on permissions, anonymous FTP may also permit uploads or modification, creating risks such as data disclosure, malware hosting, or unauthorized content changes.

### Evidence

- TCP port 21 exposed an FTP service.
- Anonymous authentication succeeded.
- The account could list and retrieve files.
- The training objective was completed; the flag value is intentionally omitted.

## Remediation

1. Disable anonymous FTP unless there is a documented business requirement.
2. Replace FTP with SFTP or another encrypted transfer method.
3. Apply least-privilege permissions to file-transfer accounts.
4. Restrict the service to approved networks and source addresses.
5. Separate public files from confidential data.
6. Monitor authentication, uploads, downloads, and unusual transfer volume.

## Defensive Detection Notes

A SOC team should investigate:

- Successful anonymous FTP logins
- File downloads from unfamiliar addresses
- Unexpected uploads or file modifications
- High-volume transfers
- FTP usage outside approved business processes
- Cleartext FTP traffic containing sensitive information

## Tools Used

- Nmap
- FTP client
- Linux command-line utilities

## Lessons Learned

This lab showed that anonymous access can turn a simple file-transfer service into a data-exposure risk. Secure file transfer requires encrypted protocols, authenticated users, least privilege, and continuous monitoring.
