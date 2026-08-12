# Hack The Box Security Report — Dancing

## Executive Summary

The Dancing lab demonstrated how an exposed Server Message Block (SMB) service and an accessible file share can disclose data without valid user credentials. Enumeration identified SMB on TCP port 445, and validation in the authorized Hack The Box environment confirmed that the WorkShares share could be accessed without authentication.

**Risk rating:** High  
**Primary weakness:** Unauthenticated access to an SMB share  
**Outcome:** Files within the exposed share were accessed in the lab

> This report documents activity performed only in an authorized Hack The Box training environment. The captured flag is intentionally omitted.

## Scope

- **Machine:** Dancing
- **Platform:** Hack The Box Starting Point
- **Difficulty:** Very Easy
- **Operating system:** Windows
- **Service assessed:** SMB
- **Authorization:** HTB lab environment

## Enumeration

An Nmap scan with default scripts and service-version detection was performed:

```bash
nmap -sC -sV -oA dancing-scan <TARGET_IP>
```

### Key Result

| Port | Protocol | Service | Observation |
|---|---|---|---|
| 445 | TCP | Microsoft-DS / SMB | File-sharing service was accessible |

Available shares were enumerated with:

```bash
smbclient -L //<TARGET_IP> -N
```

## Finding: Unauthenticated SMB Share Access

### Description

The `WorkShares` SMB share permitted access without valid credentials. Improper share and file permissions can expose internal documents or other sensitive data to unauthorized users.

### Validation

Within the authorized lab, the share was accessed with:

```bash
smbclient //<TARGET_IP>/WorkShares -N
```

The share allowed directory listing and file retrieval. The captured flag is intentionally omitted.

### Impact

An attacker who could reach the SMB service could view or retrieve exposed files. If write access were available, the attacker might also alter files, distribute malicious content, or disrupt business operations.

### Evidence

- TCP port 445 exposed an SMB service.
- Share enumeration revealed `WorkShares`.
- The share allowed access without valid credentials.
- Files could be listed and retrieved.
- The training objective was completed; the flag value is intentionally omitted.

## Remediation

1. Disable guest and anonymous SMB access.
2. Require authenticated, named user accounts.
3. Apply least-privilege share and NTFS permissions.
4. Restrict TCP port 445 to trusted internal networks.
5. Remove obsolete SMB versions and enforce SMB signing where appropriate.
6. Audit share contents and permissions regularly.
7. Monitor unusual access and bulk file retrieval.

## Defensive Detection Notes

A SOC team should investigate:

- Anonymous or guest SMB sessions
- Access to sensitive shares from unfamiliar hosts
- Repeated share enumeration
- Large numbers of file reads or downloads
- Unexpected file creation or modification
- Windows events associated with network share access, including Event IDs 5140 and 5145

## Tools Used

- Nmap
- smbclient
- Linux command-line utilities

## Lessons Learned

This lab showed that SMB enumeration is essential when port 445 is exposed. File shares should require authentication, enforce least privilege, and remain reachable only from trusted network segments.
