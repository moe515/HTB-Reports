# HTB - Explosion

## General Information:
- **Mashine Name:** Explosion
- **Difficulty:** Very Easy
- **Category:** Programming, RDP, Weak Credentials, Reconnaissance
- **IP Address:** 10.129.22.6

---
## Scanning and Enumeration:
### Nmap Scan 
```bash
nmap -sV -sC -p- -T5 -oA explosion-scan 10.129.22.6
```
### Result
- **port 3389/tcp open - ``ms-wbt-server`` (RDP)**
----
## Enumartion and Exploitation:

### Task 1:
- **What does RDP stand for ?**
``Remote Desktop Protocol``
### Task 2:
- **What is the 3-letter acronym that refers to interaction with the host through CLI ?**
``cli``
### Task 3:
- **What about graphical user interface interactions?**
``gui``
### Task 4:
- **What is the name of an old remote access tool that came without encryption by default and listens on TCP port 23?**
``telnet``
### Task 5:
- **What is the name of the service running on port 3389 TCP?**
``ms-wbt-server`` 
### Task 6:
- **What is the switch used to specify the target host's IP address when using xfreerdp?** 
``/v:``
### Task 7:
- **What username successfully returns a desktop projection to us with a blank password?**
``administrator ``
### Login RDP:
```bash
xfreerdp /v:10.129.22.6:3389 /cert:ignore /u:administrator 
```

---
## Flag:
- **Root Flag:**
```bash
951f9a6678205d1b53bab5e4eb008a80
```
----
## Note:
- **Used** ``xfreerdp`` to connect to **RDP**
- **Login** success with blank password
- **Exploitation** is due to weak credentials over **RDP**
---
## Tools Used :
- ``namp``
- ``xfreerdp``
