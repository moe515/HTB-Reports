# Hack The Box Security Report — Redeemer

## Executive Summary

The Redeemer lab demonstrated the risk of exposing a Redis database without authentication or network restrictions. Enumeration identified Redis on TCP port 6379, and validation in the authorized Hack The Box environment confirmed that an unauthenticated client could query the database and retrieve stored values.

**Risk rating:** Critical  
**Primary weakness:** Unauthenticated, remotely accessible Redis service  
**Outcome:** Database information and stored data were accessed in the lab

> This report documents activity performed only in an authorized Hack The Box training environment. The captured flag is intentionally omitted.

## Scope

- **Machine:** Redeemer
- **Platform:** Hack The Box Starting Point
- **Difficulty:** Very Easy
- **Operating system:** Linux
- **Service assessed:** Redis
- **Authorization:** HTB lab environment

## Enumeration

A full TCP port scan with default scripts and service-version detection was performed:

```bash
nmap -sC -sV -p- -oA redeemer-scan <TARGET_IP>
```

### Key Result

| Port | Protocol | Service | Observation |
|---|---|---|---|
| 6379 | TCP | Redis | Database service was remotely accessible |

## Finding: Unauthenticated Redis Access

### Description

The Redis service accepted remote client connections without requiring authentication. An unauthenticated user could query server information, enumerate database keys, and retrieve stored values.

### Validation

Within the authorized lab, a Redis session was established:

```bash
redis-cli -h <TARGET_IP>
```

The following commands were used to review the environment:

```text
INFO
SELECT 0
KEYS *
GET <KEY_NAME>
```

The client retrieved database information and stored data. The captured flag and specific sensitive value are intentionally omitted.

### Impact

An attacker could read sensitive cached data or application secrets. Depending on configuration and permissions, exposed Redis instances may also permit data modification, service disruption, persistence, or further host compromise.

### Evidence

- TCP port 6379 exposed Redis.
- The service accepted a connection without authentication.
- Server information and database keys were accessible.
- Stored values could be retrieved.
- The training objective was completed; the flag value is intentionally omitted.

## Remediation

1. Bind Redis only to trusted interfaces.
2. Restrict TCP port 6379 with host and network firewalls.
3. Enable Redis protected mode and strong authentication or ACLs.
4. Apply least-privilege permissions to application identities.
5. Use encryption for Redis traffic where supported.
6. Avoid storing unprotected secrets in memory databases.
7. Monitor administrative commands, key enumeration, and unusual client connections.
8. Keep Redis updated and follow vendor hardening guidance.

## Defensive Detection Notes

A SOC team should investigate:

- Redis connections from unfamiliar source addresses
- Remote use of commands such as `INFO`, `KEYS`, or configuration commands
- Large-scale key enumeration
- Unexpected database selection or data retrieval
- Configuration changes, persistence attempts, or service restarts
- Direct Internet exposure of TCP port 6379

## Tools Used

- Nmap
- redis-cli
- Linux command-line utilities

## Lessons Learned

This lab showed that databases should never rely on obscurity or default configurations for protection. Redis requires authentication, network isolation, secure configuration, and monitoring to prevent unauthorized access.
