# Hack The Box Security Report — Explosion

## Executive Summary

The Explosion lab demonstrated how an exposed Remote Desktop Protocol (RDP) service combined with a weak authentication configuration can allow unauthorized remote access. Enumeration identified RDP on TCP port 3389, and validation in the authorized Hack The Box environment confirmed that the Administrator account accepted a blank password.

**Risk rating:** Critical  
**Primary weakness:** Blank administrative password on an exposed remote-access service  
**Outcome:** Administrative desktop access was obtained in the lab

> This report documents activity performed only in an authorized Hack The Box training environment. The captured flag is intentionally omitted.

## Scope

- **Machine:** Explosion
- **Platform:** Hack The Box Starting Point
- **Difficulty:** Very Easy
- **Service assessed:** Remote Desktop Protocol (RDP)
- **Authorization:** HTB lab environment

## Enumeration

A full TCP port scan with default scripts and service-version detection was performed:

```bash
nmap -sV -sC -p- -T5 -oA explosion-scan <TARGET_IP>
```

### Key Result

| Port | Protocol | Service | Observation |
|---|---|---|---|
| 3389 | TCP | ms-wbt-server / RDP | Remote Desktop service was accessible |

The exposed RDP service represented the primary attack surface and required authentication testing within the authorized scope.

## Finding: Blank Administrator Password

### Description

The Windows Administrator account was configured with a blank password. This allowed an RDP session to be established without valid password authentication.

### Validation

The connection was validated with FreeRDP:

```bash
xfreerdp /v:<TARGET_IP>:3389 /cert:ignore /u:administrator
```

The command returned an interactive Windows desktop session with administrative access.

### Impact

An unauthenticated attacker who could reach the RDP service could obtain full administrative control of the host. Potential consequences include:

- Accessing or modifying sensitive data
- Installing malicious software
- Creating persistence
- Disabling security controls
- Using the host to attack other systems

### Evidence

- TCP port 3389 was open and identified as RDP.
- The Administrator account accepted a blank password.
- An administrative desktop session was successfully established.
- The training objective was completed; the flag value is intentionally omitted.

## Remediation

1. Set a long, unique password for every administrative account.
2. Prohibit blank passwords through Group Policy.
3. Restrict RDP access with host firewalls, network segmentation, or a VPN.
4. Require Network Level Authentication (NLA) and multi-factor authentication where supported.
5. Rename or disable unused default administrator accounts.
6. Monitor failed and successful RDP logons, especially Windows Event IDs 4624 and 4625.
7. Apply account lockout controls to reduce password-guessing attacks.

## Defensive Detection Notes

A SOC team should investigate:

- RDP logons from unfamiliar source addresses
- Successful logons using privileged accounts
- Repeated Event ID 4625 failures followed by Event ID 4624 success
- Logon Type 10 events associated with remote interactive sessions
- RDP activity outside approved working hours

## Tools Used

- Nmap
- FreeRDP (`xfreerdp`)
- Linux command-line utilities

## Lessons Learned

This lab showed that service exposure becomes critical when combined with weak account controls. Enumeration identified the attack surface, but the blank administrative password was the condition that turned exposure into full compromise. Remote-access services should use strong authentication, restricted network access, and continuous monitoring.
