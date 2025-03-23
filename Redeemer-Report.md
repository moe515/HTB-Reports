# HTB - Redeemer 
---

## General Information :
- **Machine Name:** Redeemer
- **Difficulty:** Very Easy
- **Operating System:** Linux
- **IP Address:** 10.129.105.16
 ---
 ## Nmap Scan 
 ```bash
 nmap -sC -sV -P- -T5 -oA rendeemer_scan 10.129.105.16
 ```
## Scan Results :
- **port 6379/tcp -->** Redis
- **Service Delected:** redis
- **No authentication required**
----
## Redis Enumeration :
```bash
redis-cli -h 10.129.105.16
```
- **Flag** ``-h`` used to specify host.
- **Used** command ``info`` to get system info.
- **Redis Version:** ``5.0.7``
- **Type:** In-memory Database.
- **selected** DB 0 using ``select 0``
- **Used** ``keys *`` to list keys
- **Found** ``4`` keys
- **Read Value -->** Found flag
 
---

## Flag :
```bash
03e1d2b376c37ab3f5319922053953eb
```
---
## Tools Used :
- ``nmap``
- ``redis-cli``
- **commands:** ``info`` , ``select`` , ``keys *`` , ``get``
---
## Notes :
- Learned about Redis default exposure.
- First hands-on Redis Enumeration. 
- Learned how to pull data from memory store
- Box showed the risk of unauthenticated Redis access.

---
## Conclusion :

Redeemer was a great exercise to understand Redis security issues.
It’s a good reminder to always secure default services and restrict access.


