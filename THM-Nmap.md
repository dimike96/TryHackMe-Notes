# THM - Nmap

[TryHackMe | Nmap](https://tryhackme.com/room/furthernmap)

> Michael Jack | 06/2022

---

## Task 1 - Deploy

This room uses a VM instance for us to mess around and learn with. We get it spun up, setup openvpn and we are ready to continue.

IP = ```10.10.207.114```

---

## Task 2 - Intro

Knowledge is power!

The enumeration stage is critical to understand what options are available, and the more we have the better.

Understanding what services are running on a potential target is critical to determining the attack surface.

> When a computer runs a network service, it opens a networking construct called a “port” to receive the connection.
> 
> Every computer has a total of 65535 available ports; however, many of these are registered as standard ports. 
> 
> For example, a HTTP Webservice can nearly always be found on port 80 of the server. A HTTPS Webservice can be found on port 443. 
> 
> Windows NETBIOS can be found on port 139 and SMB can be found on port 445. 
> 
> It is important to note; however, that especially in a CTF setting, it is not unheard of for even these standard ports to be altered, making it even more imperative that we perform appropriate enumeration on the target.

### Questions

> What networking constructs are used to direct traffic to the right application on a server?

```
ports
```

> How many of these are available on any network-enabled computer?

```
65535
```

> **[Research]** How many of these are considered "well-known"? (These are the "standard" numbers mentioned in the task)

```
1024
```

---

## Task 3 - Nmap Switches

> Nmap can be accessed by typing `nmap` into the terminal command line, followed by some of the "switches" (command arguments which tell a program to do different things) we will be covering below.
> 
> All you'll need for this is the help menu for nmap (accessed with `nmap -h`) and/or the nmap man page (access with `man nmap`). For each answer, include all parts of the switch unless otherwise specified. This includes the hyphen at the start (`-`).

### Questions

> What is the first switch listed in the help menu for a 'Syn Scan' (more on this later!)?

```
-sS
```

> Which switch would you use for a "UDP scan"?

```
-sU
```

> If you wanted to detect which operating system the target is running on, which switch would you use?

```
-O
```

> Nmap provides a switch to detect the version of the services running on the target. What is this switch?

```
-sV
```

> The default output provided by nmap often does not provide enough 
> information for a pentester. How would you increase the verbosity?

```
-v
```

> Verbosity level one is good, but verbosity level two is better! How would you set the verbosity level to two?  
> 
> (**Note**: it's highly advisable to always use *at least* this option)

```
-vv
```

> We should always save the output of our scans -- this means that we only need to run the scan once (reducing network traffic and thus chance of detection), and gives us a reference to use when writing reports for clients.
> 
> What switch would you use to save the nmap results in three major formats?

```
-oA
```

> What switch would you use to save the nmap results in a "normal" format?

```
-oN
```

> A very useful output format: how would you save results in a "grepable" format?

```
-oG
```

> Sometimes the results we're getting just aren't enough. 
> 
> If we don't care about how loud we are, we can enable "aggressive" mode. This is a shorthand switch that activates service detection, operating system detection, a traceroute and common script scanning. How would you activate this setting?

```
-A
```

> Nmap offers five levels of "timing" template. These are essentially used to increase the speed your scan runs at. Be careful though: higher speeds are noisier, and can incur errors!
> 
> How would you set the timing template to level 5?

```
-T5
```

> We can also choose which port(s) to scan. How would you tell nmap to only scan port 80?

```
-p 80
```

> How would you tell nmap to scan ports 1000-1500?

```
-p 1000-1500
```

> A very useful option that should not be ignored: How would you tell nmap to scan *all* ports?

```
-p-
```

> How would you activate a script from the nmap scripting library (lots more on this later!)?

```
--script
```

> How would you activate all of the scripts in the "vuln" category?

```
--script=vuln
```

---

## Task 4 - [Scan Types] Overview

There are different types of scans we can do with nmap. Commonly:

- TCP Connect Scans (```-sT```)

- SYN "Haalf-open" Scans (```-sS```)

- UDP Scans (```-sU```)

Additionally some less common options:

- TCP Null Scans (```-sN```)

- TCP FIN Scans (```-sF```)

- TCP Xmas Scans (```-sX```)

> Most of these (with the exception of UDP scans) are used for very similar purposes, however, the way that they work differs between each scan. This means that, whilst one of the first three scans are likely to be your go-to in most situations, it's worth bearing in mind that other scan types exist.
> 
> In terms of network scanning, we will also look briefly at ICMP (or "ping") scanning.

---

## Task 5 - [Scan Types] TCP Connect Scans

> To understand TCP Connect scans (`-sT`), it's important that you're comfortable with the *TCP three-way handshake*. If this term is new to you then completing [Introductory Networking](https://tryhackme.com/room/introtonetworking) before continuing would be advisable.

Brief overview: First the connecting machine sends a TCP request to the targer with the SYN flag set. The server responds with a TCP response that has the SYN and ACK flags set. Then the connecting machine sends a reply with the ACK flag. 

> A TCP Connect scan works by performing the three-way handshake with each target port in turn. In other words, Nmap tries to connect to each 
> specified TCP port, and determines whether the service is open by the 
> response it receives.

When a port is closed, a TCP request with the SYN flag will recieve a RST (reset) flagged response packet. This is outlined in [RFC 793](https://datatracker.ietf.org/doc/html/rfc793).

Wheras if the port is open (and accesssible) it will recive the normal SYN/ACK response.

 A port could be open but not accessible due to it being behind a firewall. 

> Many firewalls are configured to simply **drop** incoming packets. Nmap sends a TCP SYN request, and receives nothing back. This indicates that the port is
>  being protected by a firewall and thus the port is considered to be *filtered*.
> 
> That said, it is very easy to configure a firewall to respond with a RST TCP packet. For example, in IPtables for Linux, a simple version of the command would be as follows:
> 
> `iptables -I INPUT -p tcp --dport <port> -j REJECT --reject-with tcp-reset`
> 
> This can make it extremely difficult (if not impossible) to get an accurate reading of the target(s).

### Questions

> Which RFC defines the appropriate behaviour for the TCP protocol?

```
RFC 793
```

> If a port is closed, which flag should the server send back to indicate this?

```
RST
```

---

## Task 6 - [Scan Types] SYN Scans

> As with TCP scans, SYN scans (`-sS`) are used to scan the TCP port-range of a target or targets; however, the two scan types work slightly differently. 
> 
> SYN scans are sometimes referred to as "*Half-open"* scans, or *"Stealth"* scans.  
> 
> Where TCP scans perform a full three-way handshake with the target, SYN scans 
> sends back a RST TCP packet after receiving a SYN/ACK from the server (this prevents the server from repeatedly trying to make the request).

This has a variety of advantages for us as hackers:

- It can be used to bypass older Intrusion Detection systems as they are looking out for a full three way handshake. This is often no longer the case with modern IDS solutions; it is for this reason that SYN scans are still frequently referred to as "stealth" scans.

- SYN scans are often not logged by applications listening on open ports, as 
  standard practice is to log a connection once it's been fully established. 
  
  Again, this plays into the idea of SYN scans being stealthy.

- Without having to bother about completing (and disconnecting from) a three-way handshake for every port, SYN scans are significantly faster than a standard TCP Connect scan.

There are, however, a couple of disadvantages to SYN scans, namely:

- They require sudo permissions[1] in order to work correctly in Linux.
   This is because SYN scans require the ability to create raw packets (as
   opposed to the full TCP handshake), which is a privilege only the root 
  user has by default.
- Unstable services are sometimes brought down by SYN scans, which could prove problematic if a client has provided a production environment for the test.

If nmap is run with *sudo* permissions the dault is to so SYN scans. Otherwise it will default to the TCP connect scan.

Closed ports respond the same way as the TCP connect scan (RST TCP packet) the main difference is how it works with open ports.

### Questions

> There are two other names for a SYN scan, what are they?

```
half-open, stealth
```

> Can Nmap use a SYN scan without Sudo permissions (Y/N)?

```
N
```

---

## Task 7 - [Scan Types] UDP Scans

UDP connections are *stateless* unlike TCP connections which, we should recall are connection-based relying on maintaining a connection throughout the communication.

The lack of acknowledgment makes scanning UDP more difficult and take longer.

> When a packet is sent to an open UDP port, there should be no response. When this happens, Nmap refers to the port as being `open|filtered`. In other words, it suspects that the port is open, but it could be firewalled. 
> 
> If it gets a UDP response (which is very unusual), then the port is marked as *open*.
> More commonly there is no response, in which case the request is sent a second time as a double-check. If there is still no response then the port is marked *open|filtered* and Nmap moves on.  
> 
> When a packet is sent to a *closed* UDP port, the target should respond with an ICMP (ping) packet containing a message that the port is unreachable. This clearly identifies closed ports, which Nmap marks as such and moves on.

UDP scans take along time, and because of this if you are going to run them it's good practice to use ```--top-ports <number>``` to only scan some *n* most common UDP ports.

### Questions

> If a UDP port doesn't respond to an Nmap scan, what will it be marked as?

```
open|filtered
```

> When a UDP port is closed, by convention the target should send back a "port unreachable" message. Which protocol would it use to do so?

```
ICMP
```

---

## Task 8 - [Scan Types] NULL, Fin, and Xmas

> NULL, FIN and Xmas TCP port scans are less commonly used than any of the others we've covered already, so we will not go into a huge amount of depth here. All three are interlinked and are used primarily as they tend to be even 
> stealthier, relatively speaking, than a SYN "stealth" scan.

- NULL scans (```-sN```)
  
  - The TCP reqeust is sent without any flags set at all. If the port is closed the response should be a RST packet.

- FIN scans (```-sF```)
  
  - Similar to NULL except the FIN flag is set, which is normally used to gracefully close an active connection. Same RST response from closed ports.

- Xmas scans (```-sX```)
  
  - > As with the other two scans in this class, Xmas scans (`-sX`) send a malformed TCP packet and expects a RST response for closed ports. It's referred to as an xmas scan as the flags that it sets (PSH, URG and FIN) give it the appearance of a blinking christmas tree when viewed as a packet capture in Wireshark.

> Unfortunately (as with open UDP ports), that is *also* an expected behaviour if the port is protected by a firewall, so NULL, FIN and Xmas scans will only ever identify ports as being *open|filtered*, *closed*, or *filtered*.
> If a port is identified as filtered with one of these scans then it is usually because the target has responded with an ICMP unreachable packet.

Note: RFC 793 mandates that malformed packets are responded to with a RST TCP packet when closed, and not at all if open, but this isn't always the case in practice.

Windows and a lot of Cisco network devices respond with RST to any malformed packet regardless of if the port is open.

> Many firewalls are configured to drop incoming TCP packets to blocked ports which have the SYN flag set (thus blocking new connection initiation requests). By sending requests which do not contain the SYN flag, we effectively bypass this kind of firewall. Whilst this is good in theory, most modern IDS solutions are savvy to these scan types, so don't rely on them to be 100% effective when 
> dealing with modern systems.

### Questions:

> Which of the three shown scan types uses the URG flag?

```
Xmas
```

> Why are NULL, FIN and Xmas scans generally used?

```
Firewall Evasion
```

> Which common OS may respond to a NULL, FIN or Xmas scan with a RST for every port?

```
Microsoft Windows
```

---

## Task 9 - [Scan Types] ICMP Network Scanning

If we don't know much about a network one of the first things we want to do is get a map of the network structure, meaning see what IP's are active and which aren't.

We can do this is nmap to sweep through the possible IPs on the network and send them ICMP packets. When a response is recieved it marks it as alive / worth looking into further. 

We can do this using the ```-sn``` flag with a range of IP's. We can use hyphens (```-```) or CIDR notation. 

Examples: ```nmap -sn 192.168.0.1-254``` or ```nmap -sn 192.168.0.0/24```

> The `-sn` switch tells Nmap not to scan any ports -- forcing it to rely primarily on ICMP echo packets (or ARP requests on a local network, if run with sudo or directly as the root user) to identify targets. 
> 
> In addition to the ICMP echo requests, the `-sn` switch will also cause nmap to send a TCP SYN packet to port 443 of the target, as well as a TCP ACK (or TCP SYN if not run as root) packet to port 80 of the target.

### Questions

> How would you perform a ping sweep on the 172.16.x.x network (Netmask: 255.255.0.0) using Nmap? (CIDR notation)

```
nmap -sn 172.16.0.0/16
```

[Subnet Mask Cheat Sheet](https://www.aelius.com/njh/subnet_sheet.html)

---

## Task 10 - [NSE Scripts] Overview

> The **N**map **S**cripting **E**ngine (NSE) is an incredibly powerful addition to Nmap, extending its functionality quite considerably. 
> 
> NSE Scripts are written in the *Lua* programming language, and can be used to do a variety of things: from scanning for vulnerabilities, to automating exploits for them. 
> 
> The NSE is particularly useful for reconnaisance, however, it is well worth bearing
>  in mind how extensive the script library is.

There are many categories available. Some useful categories include:

- `safe`:- Won't affect the target

- `intrusive`:- Not safe: likely to affect the target  

- `vuln`:- Scan for vulnerabilities

- `exploit`:- Attempt to exploit a vulnerability

- `auth`:- Attempt to bypass authentication for running services (e.g. Log into an FTP server anonymously)

- `brute`:- Attempt to bruteforce credentials for running services

- `discovery`:- Attempt to query running services for further information about the network (e.g. query an SNMP server).

More can be found [here](https://nmap.org/book/nse-usage.html).

### Questions

> What language are NSE scripts written in?

```
lua
```

> Which category of scripts would be a *very* bad idea to run in a production environment?

```
intrusive
```

---

## Task 11 - [NSE Scripts] Working w/ the NSE

> To run a specific script, we would use `--script=<script-name>` , e.g. `--script=http-fileupload-exploiter`.
> 
> Multiple scripts can be run simultaneously in this fashion by separating them by a comma. For example: `--script=smb-enum-users,smb-enum-shares`.
> 
> Some scripts require arguments (for example, credentials, if they're exploiting an authenticated vulnerability). 
> 
> These can be given with the `--script-args` Nmap switch. 
> 
> An example of this would be with the `http-put` script (used to upload files using the PUT method). This takes two arguments: the URL to upload the file to, and the file's location on disk.

Full list of scripts can be found [here](https://nmap.org/nsedoc/).

### Questions

> What optional argument can the `ftp-anon.nse` script take?

[ftp-anon NSE script &mdash; Nmap Scripting Engine documentation](https://nmap.org/nsedoc/scripts/ftp-anon.html)

```
maxlist
```

---

## Task 12 - [NSE Scripts] Searching for Scripts

How can we find scripts to use with nmap? 

> We have two options for this, which should ideally be used in conjunction with each other. The first is the page on the [Nmap website](https://nmap.org/nsedoc/) (mentioned in the previous task) which contains a list of all official scripts. 
> 
> The second is the local storage on your attacking machine. Nmap stores its scripts on Linux at `/usr/share/nmap/scripts`. 
> 
> All of the NSE scripts are stored in this directory by default -- this is where Nmap looks for scripts when you specify them.
> 
> There are two ways to search for installed scripts. One is by using the `/usr/share/nmap/scripts/script.db` file. Despite the extension, this isn't actually a database so much as a formatted text file containing filenames and categories for each available script.

We can also use "grep" with that scripts.db file to search through it, or go to the directory and run an ```ls```. An example of an ls searching for a category:

 ```ls -l /usr/share/nmap/scripts/*ftp*```

> It's also possible to install the scripts manually by downloading the script from Nmap (`sudo wget -O /usr/share/nmap/scripts/<script-name>.nse https://svn.nmap.org/nmap/scripts/<script-name>.nse`). 
> 
> This must then be followed up with `nmap --script-updatedb`, which updates the `script.db` file to contain the newly downloaded script.
> 
> It's worth noting that you would require the same "updatedb" command if you 
> were to make your own NSE script and add it into Nmap -- a more than manageable task with some basic knowledge of Lua!

### Questions

> Search for "smb" scripts in the `/usr/share/nmap/scripts/` directory using either of the demonstrated methods. 
> 
> What is the filename of the script which determines the underlying OS of the SMB server?

```shell
ls -l /usr/share/nmap/scripts/*smb*
```

```
smb-os-discovery.nse
```

> Read through this script. What does it depend on?

```
smb-brute
```

---

## Task 13 - Firewall Evasion

Stealth scans, NULL, FIN, and Xmas scans are good and useful, but there is another common configuration we should learn about.

> Your typical Windows host will, with its default firewall, block all 
> ICMP packets. 
> 
> This presents a problem: not only do we often use *ping* to manually establish the activity of a target, Nmap does the same thing by default. 
> 
> This means that Nmap will register a host with this firewall configuration as dead and not bother scanning it at all.

Nmap does have an option to get around this. We can use ```-Pn``` which makes nmap skip pinging hosts before scanning them. It treats all hosts as alive and because of this it gets past the ICMP block, but will take way longer as it's going try and retry ports that are closed. 

> It's worth noting that if you're already directly on the local network, Nmap can also use ARP requests to determine host activity.

Nmap has a variety of other switches that can be useful in firewall evasion.

Some of them:

> - `-f`:- Used to fragment the packets (i.e. split 
>   them into smaller pieces) making it less likely that the packets will be
>    detected by a firewall or IDS.
> - An alternative to `-f`, but providing more control over the size of the packets: `--mtu <number>`, accepts a maximum transmission unit size to use for the packets sent. This *must* be a multiple of 8.
> - `--scan-delay <time>ms`:-
>    used to add a delay between packets sent. This is very useful if the 
>   network is unstable, but also for evading any time-based firewall/IDS 
>   triggers which may be in place.
> - `--badsum`:- this is 
>   used to generate in invalid checksum for packets. Any real TCP/IP stack 
>   would drop this packet, however, firewalls may potentially respond 
>   automatically, without bothering to check the checksum of the packet. As
>    such, this switch can be used to determine the presence of a 
>   firewall/IDS.

### Questions

> Which simple (and frequently relied upon) protocol is often blocked, requiring the use of the `-Pn` switch?

```
ICMP
```

> **[Research]** Which Nmap switch allows you to append an arbitrary length of random data to the end of packets?

```
--data-length
```

---

## Task 14 - Practical

### Questions

> Does the target (`MACHINE_IP`)respond to ICMP (ping) requests (Y/N)?

```shell
ping 10.10.207.114
```

```
N
```

> Perform an Xmas scan on the first 999 ports of the target -- how many ports are shown to be open or filtered?

```shell
 ╭─michaelj@MJ in ~/Documents/IT and Cyber Self Study /THM took 3m22s
 ╰─λ sudo nmap -sX -p 1-999 -vv 10.10.211.187
Starting Nmap 7.92 ( https://nmap.org ) at 2022-06-04 04:10 EDT
Initiating Ping Scan at 04:10
Scanning 10.10.211.187 [4 ports]
Completed Ping Scan at 04:10, 3.01s elapsed (1 total hosts)
Nmap scan report for 10.10.211.187 [host down, received no-response]
Read data files from: /usr/bin/../share/nmap
Note: Host seems down. If it is really up, but blocking our ping probes, try -Pn
Nmap done: 1 IP address (0 hosts up) scanned in 3.20 seconds
           Raw packets sent: 8 (304B) | Rcvd: 0 (0B)
```

This did really explicitly say anything useful. 4 ports? Should I assume from this all ports are ```open|filtered```?

```shell
 ╭─michaelj@MJ in ~/Documents/IT and Cyber Self Study /THM took 46s
 ╰─λ sudo nmap -sX -Pn -p 1-999 -vv 10.10.211.187 | tee nmap_xmas-scan.log
Starting Nmap 7.92 ( https://nmap.org ) at 2022-06-04 04:05 EDT
Initiating Parallel DNS resolution of 1 host. at 04:05
Completed Parallel DNS resolution of 1 host. at 04:05, 1.07s elapsed
Initiating XMAS Scan at 04:05
Scanning 10.10.211.187 [999 ports]
XMAS Scan Timing: About 15.52% done; ETC: 04:09 (0:02:49 remaining)
XMAS Scan Timing: About 30.53% done; ETC: 04:09 (0:02:19 remaining)
XMAS Scan Timing: About 45.55% done; ETC: 04:09 (0:01:49 remaining)
XMAS Scan Timing: About 60.56% done; ETC: 04:09 (0:01:19 remaining)
Stats: 0:02:08 elapsed; 0 hosts completed (1 up), 1 undergoing XMAS Scan
XMAS Scan Timing: About 63.06% done; ETC: 04:09 (0:01:14 remaining)
XMAS Scan Timing: About 78.58% done; ETC: 04:09 (0:00:43 remaining)
Completed XMAS Scan at 04:09, 201.21s elapsed (999 total ports)
Nmap scan report for 10.10.211.187
Host is up, received user-set.
Scanned at 2022-06-04 04:05:42 EDT for 201s
All 999 scanned ports on 10.10.211.187 are in ignored states.
Not shown: 999 open|filtered tcp ports (no-response)

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 202.47 seconds
           Raw packets sent: 1998 (79.920KB) | Rcvd: 0 (0B)
```

Adding the ```-Pn``` flag took way too long but actuall says 999 open|filtered tcp ports.

```
999
```

> There is a reason given for this -- what is it? **Note:** The answer will be in your scan results. Think carefully about which switches to use -- and read the hint before asking for help!

```
no response
```

> Perform a TCP SYN scan on the first 5000 ports of the target -- how many ports are shown to be open?

```shell
 ╭─michaelj@MJ in ~/Documents/IT and Cyber Self Study /THM took 50s
 ╰─λ sudo nmap -sS -Pn -p 1-5000 -vv 10.10.211.187 | tee nmap_syn-scan.log
Starting Nmap 7.92 ( https://nmap.org ) at 2022-06-04 04:04 EDT
Initiating Parallel DNS resolution of 1 host. at 04:04
Completed Parallel DNS resolution of 1 host. at 04:04, 1.04s elapsed
Initiating SYN Stealth Scan at 04:04
Scanning 10.10.211.187 [5000 ports]
Discovered open port 21/tcp on 10.10.211.187
Discovered open port 53/tcp on 10.10.211.187
Discovered open port 3389/tcp on 10.10.211.187
Discovered open port 80/tcp on 10.10.211.187
Discovered open port 135/tcp on 10.10.211.187
Completed SYN Stealth Scan at 04:04, 45.26s elapsed (5000 total ports)
Nmap scan report for 10.10.211.187
Host is up, received user-set (0.28s latency).
Scanned at 2022-06-04 04:04:08 EDT for 45s
Not shown: 4995 filtered tcp ports (no-response)
PORT     STATE SERVICE       REASON
21/tcp   open  ftp           syn-ack ttl 125
53/tcp   open  domain        syn-ack ttl 125
80/tcp   open  http          syn-ack ttl 125
135/tcp  open  msrpc         syn-ack ttl 125
3389/tcp open  ms-wbt-server syn-ack ttl 125

Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 46.49 seconds
           Raw packets sent: 10022 (440.968KB) | Rcvd: 32 (1.408KB)
```

```
5
```

> Motitor with wireshark and make sure you understand what happens when you do a TCP connect scan against port 80.

> Deploy the `ftp-anon` script against the box. Can Nmap login successfully to the FTP server on port 21? (Y/N)

```shell
 ╭─michaelj@MJ in ~/Documents/IT and Cyber Self Study /THM took 3ms
 ╰─λ cat nmap_ftp-anon-script.log 
File: nmap_ftp-anon-script.log
Starting Nmap 7.92 ( https://nmap.org ) at 2022-06-04 04:14 EDT
NSE: Loaded 1 scripts for scanning.
NSE: Script Pre-scanning.
NSE: Starting runlevel 1 (of 1) scan.
Initiating NSE at 04:14
Completed NSE at 04:14, 0.00s elapsed
Initiating Ping Scan at 04:14
Scanning 10.10.211.187 [2 ports]
Completed Ping Scan at 04:14, 0.13s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 04:14
Completed Parallel DNS resolution of 1 host. at 04:14, 1.04s elapsed
Initiating Connect Scan at 04:14
Scanning 10.10.211.187 [1000 ports]
Discovered open port 21/tcp on 10.10.211.187
Discovered open port 135/tcp on 10.10.211.187
Discovered open port 80/tcp on 10.10.211.187
Discovered open port 3389/tcp on 10.10.211.187
Discovered open port 53/tcp on 10.10.211.187
Completed Connect Scan at 04:15, 7.74s elapsed (1000 total ports)
NSE: Script scanning 10.10.211.187.
NSE: Starting runlevel 1 (of 1) scan.
Initiating NSE at 04:15
Completed NSE at 04:15, 30.61s elapsed
Nmap scan report for 10.10.211.187
Host is up, received syn-ack (0.13s latency).
Scanned at 2022-06-04 04:14:58 EDT for 38s
Not shown: 995 filtered tcp ports (no-response)
PORT     STATE SERVICE       REASON
21/tcp   open  ftp           syn-ack
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: TIMEOUT
53/tcp   open  domain        syn-ack
80/tcp   open  http          syn-ack
135/tcp  open  msrpc         syn-ack
3389/tcp open  ms-wbt-server syn-ack

NSE: Script Post-scanning.
NSE: Starting runlevel 1 (of 1) scan.
Initiating NSE at 04:15
Completed NSE at 04:15, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 39.78 seconds
```

```
Y
```

---

## Task 15 - Conclusion

> There are lots of great resources for learning more about Nmap on your own. Front and center are Nmaps own (highly extensive) [docs](https://nmap.org/book/) which have already been mentioned several times throughout the room. 
> These are a superb resource, so, whilst reading through them line-by-line and learning them by rote is entirely unnecessary, it would be highly advisable to use them as a point of reference, should you need it.

---
