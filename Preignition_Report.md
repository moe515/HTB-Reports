# HTB Report - Preignition

## General Information
- **Machine Name**: Preignition
- **Difficulty**: Very Easy
- **IP Address**: *Displayed on HTB when machine is spawned*
- **Tags**: Custom Applications, Apache, Reconnaissance, Web Site Structure Discovery, Default Credentials

## Scanning and Enumeration
- Ran `nmap -sV -Pn -p- -T5 -oA preignition-scan 10.129.116.87` to identify open ports and services.
- Found **Port 80/tcp** open, running **nginx 1.14.2**.
- Navigated to the web interface and discovered it’s a login panel.

## Directory Bruteforcing
- Used **Gobuster** for directory enumeration:
  ```bash
  gobuster dir -u http://10.129.116.87 -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt -x .php
  ```
- Discovered page: `admin.php`
- Status Code: **200 OK**

## Exploitation
- Tried default credentials on `admin.php`:
  - **Username**: `admin`
  - **Password**: `admin`
- Successfully logged into the admin panel.

## Privilege Escalation
- No further escalation needed as admin login directly revealed the flag.

## Flag
- **Root Flag**: `6435bbe007c10d157f1446bd017503673`

## Tools Used
- nmap
- gobuster
- web browser
- seclists **-wordlists**
## Notes
- Always test default credentials for admin pages.
- Gobuster is effective for discovering hidden directories.
