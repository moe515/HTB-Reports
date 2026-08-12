# Hack The Box Security Reports

A collection of hands-on Hack The Box Starting Point reports documenting my methodology, tools, findings, and lessons learned.

> **Ethical use:** These reports are based on authorized training environments. The techniques documented here should only be used on systems you own or have explicit permission to test.

## Reports

| Machine | Primary Focus | Report |
|---|---|---|
| Meow | Service enumeration and Telnet | [View report](Meow_Report.md) |
| Fawn | FTP enumeration and access | [View report](Fawn_Report.md) |
| Dancing | SMB enumeration and file shares | [View report](Dancing_Report.md) |
| Redeemer | Redis enumeration | [View report](Redeemer-Report.md) |
| Explosion | RDP enumeration and weak authentication | [View report](Explosion-Report.md) |
| Preignition | Web enumeration and default credentials | [View report](Preignition_Report.md) |

## Methodology

Each lab follows a repeatable workflow:

1. Define the authorized target and scope.
2. Perform reconnaissance and service enumeration.
3. Investigate exposed services and potential attack paths.
4. Validate findings in the lab environment.
5. Document evidence, impact, and lessons learned.
6. Recommend defensive controls where applicable.

## Tools Demonstrated

- Nmap
- Gobuster
- SMB client tools
- FTP, Telnet, RDP, and Redis clients
- Linux command-line utilities
- Web browser and manual validation

## Skills Demonstrated

- Network and service enumeration
- Web content discovery
- Default-credential testing
- Misconfiguration identification
- Evidence collection
- Technical security reporting

## Planned Improvements

- Add executive summaries and risk ratings
- Add remediation guidance to every report
- Remove training flags and sensitive lab answers
- Add SOC-focused detections and defensive observations
- Standardize report formatting

## Disclaimer

This repository is for education and portfolio demonstration only. Do not use these techniques without authorization.
