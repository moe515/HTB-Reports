# HTB - Meow 

---
##  general information:
- **Machine Name:** Meow
- **Difficulty:** Very Easy
- **Operating System:** Linux
- **IP Address:** 10.129.32.149
---
## Nmap Scan:
```bash
nmap -sC -sV -oA meow_scan 10.129.32.149
```
## Scan Results:
- **Port 23/tcp -->telnet (No authentication)**
---
## Access Method:
```bash
telnet 10.129.32.149
```
- logged in as ``root``
- connected directly without **password**
---
## Flag:
```bash
cat flag.txt
```
- **Results** : ``b40abdfe23665f766f9c61ecba8a4c19``

---
## Tools Used: 
- nmap 
- telnet
- ping
- openvpn
---
## Notes:
- This was my first machine on Hack The Box.
- I learned how to use `nmap` to scan for open ports.
- I understood how to find and read the flag. 
- It gave me confidence to continue learning.
---
## Conclusion:
Meow was a great starting point for learning how Hack The Box works.
It was simple, didn't require any exploit, and helped me get familliar with scanning, basic access, and flag capturing.
I'm now ready to move on to more challenging boxees. 