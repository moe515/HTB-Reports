# Hack The Box Security Reports

A collection of hands-on Hack The Box Starting Point reports documenting my methodology, tools, findings, defensive observations, and lessons learned.

> **Ethical use:** These reports are based on authorized training environments. The techniques documented here should only be used on systems you own or have explicit permission to test.

## Reports

| Machine | Primary Focus | Risk Rating | Report |
|---|---|---|---|
| Meow | Unauthenticated Telnet access | Critical | [View report](Meow_Report.md) |
| Fawn | Anonymous FTP file access | High | [View report](Fawn_Report.md) |
| Dancing | Unauthenticated SMB share access | High | [View report](Dancing_Report.md) |
| Redeemer | Unauthenticated Redis exposure | Critical | [View report](Redeemer-Report.md) |
| Explosion | Blank-password RDP access | Critical | [View report](Explosion-Report.md) |
| Preignition | Default web-admin credentials | High | [View report](Preignition_Report.md) |

## Methodology

Each lab follows a repeatable workflow:

1. Define the authorized target and scope.
2. Perform reconnaissance and service enumeration.
3. Investigate exposed services and potential attack paths.
4. Validate findings in the lab environment.
5. Document evidence and business impact.
6. Recommend remediation and defensive detection opportunities.
7. Record lessons learned.

## Report Standards

Every report includes:

- Executive summary and risk rating
- Scope and authorization statement
- Enumeration methodology
- Security finding and supporting evidence
- Impact analysis
- Remediation guidance
- SOC detection notes
- Lessons learned

Training flags, live lab addresses, and sensitive answer values are intentionally omitted.

## Tools Demonstrated

- Nmap
- Gobuster and SecLists
- Telnet and FTP clients
- smbclient
- redis-cli
- FreeRDP
- Linux command-line utilities
- Web browser and manual validation

## Skills Demonstrated

- Network and service enumeration
- Web content discovery
- Authentication and access-control testing
- Misconfiguration identification
- Evidence collection
- Risk assessment
- Remediation planning
- Defensive detection thinking
- Technical security reporting

## Disclaimer

This repository is for education and portfolio demonstration only. Do not use these techniques without authorization.
