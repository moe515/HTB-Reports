# HTB - Dancing 
---
## General Information :
- **Machine Name:** Dancing
- **Difficulty:** Very Easy 
- **Operating System:** Windows
- **IP Address:** 10.129.121.19

---
## Nmap Scan :
```bash 
nmap -sC -sV -oA dansing_scan 10.129.121.19  
```
## scan Results :
- **Port 445/tcp** --> **microsoft-ds**
- **Service:** ``SMB`` (SERVER MESSAGE BLOCK)
- **OS Detected:** Windows / Unix-like
- **Shares** avaiable without credentials
---
## Access via ``SMB`` :
```bash
smbclient -L 10.129.121.19 
```
- **I get 4 user 3 with password and 1 without password :** ``WorkShares``
```bash
smbclient \\\\10.129.121.19\\WorkShares
```
- **Accessed** share WorkShares
- **Used** ``ls`` to list files
- **Used** ``get`` to download flag file
---
## Flag :
```bash
cat flag.txt
```
- **Result:** ``5f61c10dffbc77a704d76016a22f1664``
---
## Tools Used :
- ``nmap``
- ``smbclient``
- ``ls``,``get``,``cat``
- ``ping``
---
## Notes :
- **Learned** about ``SMB`` enumeration and shares .
- **Understood** anonymous acces to pubblic shares .
- **First Time** using smbclient
- **Easy And Smooth Box**, good for learning basics of ``smb``
---
## Conclusion :  
Dancing was a smooth introduction to SMB and Windows-based boxes.
It showed how some systems expose shares without authentication, and how to retrieve flags using simple enumeration.