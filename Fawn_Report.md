# HTB - Fawn
---
## General Information :
- **Machine Name:** Fawn
- **Difficulty:** Very Easy
- **Operating System:** Linux 
- **IP Address:** 10.129.120.201
---
## Nmap Scan : 
```bash
Nmap -sC -sV -oA fawn_scan 10.129.120.201
```
## Scan Results :
- port 21/tcp --> FTP
- login allowed ``Anonymous``
---
## Access : 
```bash
ftp -v 10.129.120.201
```
- Logged in as : ``anonymous``
- password in as: ``password``
- Response Code: ``230`` (Login Successful)
- Used ``ls`` to list files
- Used ``get`` to download flag file
---
## Flag :
```bash
cat flag.txt
```
- Results : ``035db21c881520061c53e0536e44f815``
---
## Tools Used :
- nmap
- ftp 
- ping
- get , ls , ftp help ``?`` , cat
---
## Notes :
- First time interacting with FTP in CTF context
- Learned how anonymous login works
- Understood FTP commands : ``ls`` , ``get`` ,``?``
- Learned about protocol weaknesses (no encryption)
---
## Conclusion :
Fawn was a very basic FTP box. Great for understanding FTP services, anonymous access, and how to retrieve files manually.