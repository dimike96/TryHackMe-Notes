# THM - Nmap Live Host Discovery

[TryHackMe | Nmap Live Host Discovery](https://tryhackme.com/room/nmap01)

> Michael Jack | 06/2022

---

## Task 1 - Introduction

> When we want to target a network, we want to find an efficient tool to help us handle repetitive tasks and answer the following questions:
> 
> 1. Which systems are up?
> 2. What services are running on these systems?

> We present the different approaches that Nmap uses to discover live hosts. In particular: 
> 
> 1. ARP scan: This scan uses ARP requests to discover live hosts
> 2. ICMP scan: This scan uses ICMP requests to identify live hosts
> 3. TCP/UDP ping scan: This scan sends packets to TCP ports and UDP ports to determine live hosts.

Also introduced are ```arp-scan``` and ```masscan```, and how they overlap with part of nmap host discovery.

---

## Task 2 - Subnetworks

> A *network segment* is a group of computers connected using a shared medium. For instance, the medium can be the Ethernet switch or WiFi access point. 
> 
> In an IP network, a *subnetwork* is usually the equivalent of one or more network segments connected together and configured to use the same router. 
> 
> The network segment refers to a physical connection, while a subnetwork refers to a logical connection.

A subnet has it's own IP range, and is connected to a more extensive network through the router. 

There can be different types of subnets. For example a ```/16``` subnet would have a mask written like ```255.255.0.0``` and can support around 65k hosts, wheras a ```/24``` subnet would have a mask written like ```255.255.255.0``` and can only support around 250 hosts.

Task 2 in this room is also useful to refresh on subnetting: [TryHackMe | Intro to LAN](https://tryhackme.com/room/introtolan)

### Questions

> Send an ARP Request from computer1 in the network simulator with computer6 as the data (we want it's MAC). How many devices can see it?

```
4
```

> Did computer6 receive the ARP Request? (Y/N)

```
N
```

> Now from computer 4 send an ARP Request. How many devices can see it?

```
4
```

> Did computer6 reply to the ARP Request? (Y/N)

```
Y
```

---

## Task 2 - Enumerating Targets

If we want to use the different methods of scanning we need to specify the target(s) we want to scan.

> Generally speaking, you can provide a list, a range, or a subnet.

Some examples of these methods:

```
10.10.10.10 scan.nmap.org example.com // A list that will scan 3 addresses
10.12.13.15-20 // A range that will scan 6 addresses
10.10.10.10/30 // A subnet that will scan 4 addresses
```

### Questions

> What is the first IP nmap would scan if you provide ```10.10.12.13/29``` as your target?

```shell
nmap -sL -n 10.10.12.13/29
Starting Nmap 7.92 ( https://nmap.org ) at 2022-06-02 03:59 EDT
Nmap scan report for 10.10.12.8
Nmap scan report for 10.10.12.9
Nmap scan report for 10.10.12.10
Nmap scan report for 10.10.12.11
Nmap scan report for 10.10.12.12
Nmap scan report for 10.10.12.13
Nmap scan report for 10.10.12.14
Nmap scan report for 10.10.12.15
Nmap done: 8 IP addresses (0 hosts up) scanned in 0.00 seconds
```

```
10.10.12.8
```

> How many IP addresses will Nmap scan if you provide the following range `10.10.0-255.101-125`?

```shell
nmap -sL -n 10.10.0-255.101-125
...
# Removed the 6.4k addresses
...
Nmap done: 6400 IP addresses (0 hosts up) scanned in 0.02 seconds
```

```
6400
```

---

## Task 4 - Discovering Live Hosts

Let's conside the TCP/IP layers. We can leverage the protocols to discover live hosts. 

From bottom up we can use:

- ARP from the link layer
  
  - Used to send a frame to the broadcast addess on the network segmeet and asking the computer which IP address to respond by providing it's MAC address.

- ICMP from the network layer
  
  - Has many types ([Internet Control Message Protocol (ICMP) Parameters](https://www.iana.org/assignments/icmp-parameters/icmp-parameters.xhtml))
  
  - ICMP ping uses type 8 (Echo) and type 0 (Echo Reply)

- TCP and UDP from the transport layer
  
  - Scanners can send specially crafted packets to common ports to see if they respond. Efficient, especially when ICMP echo is blocked.

### Questions

> Send a packet from computer1 to computer3 that's a ping request. What is the type of packet that computer1 sends before the ping?    

```
ARP request
```

> What is the type of packet that computer1 received before being able to send the ping?

```
ARP response
```

> How many computer responded to the ping request?

```
1
```

> Send a packet from computer2 to computer5 that is a ping request. What is the first device that responds to the first ARP request?

```
Router
```

> What is the first device that responds to the second ARP request?

```
Computer5
```

> Send another ping request. DId it require a new ARP request?

```
N
```

---

## Task 5 - Host Discovery Using ARP

> When no host discovery options are provided, Nmap follows the following approaches to discover live hosts:
> 
> 1. When a *privileged* user tries to scan targets on a local network (Ethernet), Nmap uses *ARP requests*. A privileged user is `root` or a user who belongs to `sudoers` and can run `sudo`.
> 2. When a *privileged* user tries to scan targets outside the local network, Nmap uses ICMP echo requests, TCP ACK (Acknowledge) to port 80, TCP SYN (Synchronize) to port 443, and ICMP timestamp request.
> 3. When an *unprivileged* user tries to scan targets outside the local network, Nmap resorts to a TCP 3-way handshake by sending SYN packets to ports 80 and 443.

By default nmap used a ping scan to find live hosts. Then it proceeds to scan only live hosts. If we want to discover hosts that are online without port-scanning them afterwards we can use ```nmap -sn TARGETS```. 

> ARP scan is possible only if you are on the same subnet as the target 
> systems. On an Ethernet (802.3) and WiFi (802.11), you need to know the MAC address of any system before you can communicate with it. 
> 
> The MAC address is necessary for the link-layer header; the header contains the source MAC address and the destination MAC address among other fields. To get the MAC address, the OS sends an ARP query. 
> 
> A host that replies to ARP queries is up. The ARP query only works if the target is on the same subnet as yourself, i.e., on the same Ethernet/WiFi. 
> 
> You should expect to see many ARP queries generated during a Nmap scan of a local network. If you want Nmap only to perform an ARP scan without port-scanning, you can
>  use `nmap -PR -sn TARGETS`, where `-PR` indicates that you only want an ARP scan. 

When scanning we send out ARP requests to all of our targets and for each request the host with the IP address we are asking about will send an ARP reply with its MAC address, and that’s how we will know that it is online.

> Talking about ARP scans, we should mention a scanner built around ARP queries: `arp-scan`; it provides many options to customize your scan. 
> 
> Visit the [arp-scan wiki](http://www.royhills.co.uk/wiki/index.php/Main_Page) for detailed information. One popular choice is `arp-scan --localnet` or simply `arp-scan -l`. This command will send ARP queries to all valid IP addresses on your local networks.
> 
> Moreover, if your system has more than one interface and you are interested in discovering the live hosts on one of them, you can specify the interface using
> 
> `-I`. For instance, `sudo arp-scan -I eth0 -l` will send ARP queries for all valid IP addresses on the `eth0` interface.

### Questions

> Send an ARP request from computer1 to computer1 (to indicat it is broadcast). Try all the possible devices on the network (8). How many are you able to discover using ARP requests?

```
3
```

---

## Task 6 - Nmap Host Discovery Using ICMP

> We can ping every IP address on a target network and see who would respond to our `ping` (ICMP Type 8/Echo) requests with a ping reply (ICMP Type 0). 
> 
> Simple, isn’t it? Although this would be the most straightforward approach, it is not always reliable. Many firewalls block ICMP echo; new versions of MS Windows are configured with a host firewall that blocks ICMP echo requests by default. 
> 
> Remember that an ARP query will precede the ICMP request if your target is on the same subnet.
> 
> To use ICMP echo request to discover live hosts, add the option `-PE`. (Remember to add `-sn` if you don’t want to follow that with a port scan.) 
> 
> An ICMP echo scan works by sending an ICMP echo request and expects the target to reply with an ICMP echo reply if it is online.

Because ICMP echo requests tend to be blocked, you might also consider ICMP Timestamp or ICMP Address Mask requests to tell if a system is online. 

Nmap uses timestamp request (ICMP Type 13) and checks whether it will get a Timestamp
reply (ICMP Type 14). Adding the `-PP` option tells Nmap to use ICMP timestamp requests. 

Nmap uses address mask queries (ICMP Type 17) and checks whether it gets an address mask reply (ICMP Type 18). This scan can be enabled with the option `-PM`.

> It is essential to learn multiple approaches to achieve the same result. If one type of packet is being blocked, we can always choose another to discover the target network and services.

### Questions

> What is the option to tell nmap to use ICMP timestamp to discover live hosts?

```
-PP
```

> What is the option required to tell Nmap to use ICMP Address Mask to discover live hosts?

```
-PM
```

> What is the option required to tell Nmap to use ICMP Echo to discover life hosts?

```
-PE
```

---

## Task 7 - Nmap Host Discovery Using TCP and UDP

One option is using a TCP SYN ping.

> We can send a packet with the SYN (Synchronize) flag set to a TCP port, 80 by default, and wait for a response. 
> 
> An open port should reply with a SYN/ACK (Acknowledge); a closed port would result in an RST (Reset). In this case, we only check whether we will get any response to infer whether the host is up. 
> 
> The specific state of the port is not significant here.
> 
> If you want Nmap to use TCP SYN ping, you can do so via the option `-PS` followed by the port number, range, list, or a combination of them. 
> 
> For example, `-PS21` will target port 21, while `-PS21-25` will target ports 21, 22, 23, 24, and 25. Finally `-PS80,443,8080` will target the three ports 80, 443, and 8080.
> 
> Privileged users (root and sudoers) can send TCP SYN packets and don’t need to complete the TCP 3-way handshake even if the port is open. 
> 
> Unprivileged users have no choice but to complete the 3-way handshake if the port is open.

We can also use TCP ACK ping. 

> As you have guessed, this sends a packet with an ACK flag set. 
> 
> You must be running Nmap as a privileged user to be able to accomplish this. 
> 
> If you try it as an unprivileged user, Nmap will attempt a 3-way handshake.
> 
> By default, port 80 is used. The syntax is similar to TCP SYN ping. `-PA` should be followed by a port number, range, list, or a combination of them. 
> 
> For example, consider `-PA21`, `-PA21-25` and `-PA80,443,8080`. If no port is specified, port 80 will be used.

Further, we could use UDP ping.

> Contrary to TCP SYN ping, sending a UDP packet to an open port is not expected to lead to any reply. 
> 
> However, if we send a UDP packet to a closed UDP port, we expect to get an ICMP port unreachable packet; this indicates that the target system is up and available.
> 
> However, sending a UDP packet to any closed UDP port can trigger a response indirectly indicating that the target is online.
> 
> The syntax to specify the ports is similar to that of TCP SYN ping and TCP ACK ping; Nmap uses `-PU` for UDP ping.

**Masscan**

On a side note, Masscan uses a similar approach to discover the available systems. However, to finish its network scan quickly, Masscan is quite aggressive with the rate of packets it generates. The syntax is quite similar: `-p` can be followed by a port number, list, or range. Consider the following examples:

- `masscan MACHINE_IP/24 -p443`
- `masscan MACHINE_IP/24 -p80,443`
- `masscan MACHINE_IP/24 -p22-25`
- `masscan MACHINE_IP/24 ‐‐top-ports 100`

### Questions

> Which TCP ping scan does not require a privileged account?

```
TCP SYN ping
```

> Which TCP ping scan requires a privileged account?

```
TCP ACK ping
```

> What option do you need to add to Nmap to run a TCP SYN ping scan on the telnet port?

```
-ps23
```

---

## Task 8 - Using Reverse-DNS Lookup

> Nmap’s default behaviour is to use reverse-DNS online hosts. 
> 
> Because the hostnames can reveal a lot, this can be a helpful step. 
> 
> However, if you don’t want to send such DNS queries, you use `-n` to skip this step.
> 
> By default, Nmap will look up online hosts; however, you can use the option `-R` to query the DNS server even for offline hosts. If you want to use a specific DNS server, you can add the `--dns-servers DNS_SERVER` option.

### Questions

> We want Nmap to issue a reverse DNS lookup for all the possibles hosts on a subnet, hoping to get some insights from the names. What option should we add?

```
-R
```

---

## Task 9 - Summary

> You have learned how ARP, ICMP, TCP, and UDP can detect live hosts by completing this room. Any response from a host is an indication that it is online.
> 
> Remember to add `-sn` if you are only interested in host discovery without port-scanning. Omitting `-sn` will let Nmap default to port-scanning the live hosts.

---
[[General-Skills/Linux/Command Reference Library/nmap]]
[[THM-Nmap]]