# THM Introductory Networking

[TryHackMe | Introductory Networking](https://tryhackme.com/room/introtonetworking)

> Michael Jack | 06/2022

---

## Task 1 - Intro

> The topics that we're going to cover in this room are:
> 
> - The OSI Model
> - The TCP/IP Model
> - How these models look in practice
> - An introduction to basic networking tools

---

## Task 2 - The OSI Model: An Overview

The OSI model consists of seven layers:

- **7 - Application**
  
  - Provides networking options to programs running on a computer. Works almost only with applications, passes data to the presentation layer.

- **6 - Presentation**
  
  - Translates data from the application layer into a standardized format, handles encryption, compression, or other transformations to the data. Passes data to the session layer.

- **5 - Session**
  
  - If the data from the presentation layer is in the correct from, it tries to establish the connection across the network to another machine. IF it can it's job is to maintain the connection, else it returns an error. The session is unique to the particular communication occuring. Once the connection is successfully logged it passes data to the transport layer.

- **4 - Transport**
  
  - The transport layer is very important and server several functions.
    
    - Chooses the protocol
      
      - **TCP** (Transmission Control Protocol) - Transmission is connection based. For the duration of the request a connection is established and maintained. All data can be verified to be recieved. Accuracy over speed.
      
      - **UDP** (User Datagram Protocol) - Packets are essentially "thrown" at the recieving computer. Speed over accuracy, as data can be lost.
    
    - Divides the transmittion into bite-sized pieces (**segments** when working with TCP and **datagrams** when working with UDP).

- **3 - Network**
  
  - The network layer locates the destination of the request, and figures out the best route to take to get there. This uses IP addresses in was is referred to ad *logical addressing*, which is software controlled. IPv4 is the most common form of logical addressing as an example.

- **2 - Data Link**
  
  - This is where it switches to *physical addressing* using **MAC** (Media Access Control) address. 
  
  - > MAC addresses are set by the manufacturer and literally burnt into the card; they can't be changed -- although they *can* be spoofed. When information is sent across a network, it's actually the physical address that is used to identify where exactly to send the information.
  
  - It also makes sure data is in the correct format for transmission, and makes sure that recieved data hasn't been corrupted.

- **1 - Physical**
  
  - This is the physical hardware of the computers on the network. The electrical pulses that are sent and recieved. This layer converts the binary data of the transmission to signals to send accross the cables, routers, switches, etc. that make up the network.

> There are many mnemonics floating around to help you learn the layers
>  of the OSI model -- search around until you find one that you like.
> 
> I personally favour: **A**nxious **P**ale **S**hakespeare **T**reated **N**ervous **D**runks **P**atiently

"Please Do Not Teach Stupid People Acronyms"

"A Penguin Said that Nobody Drinks Pepsi"

> Q: Which layer would choose to send data over TCP or UDP?

```
4
```

> Q: Which layer checks recieved packets to make sure that they haven't been corrupted?

```
2
```

> Q: In which layer would data be formatted in preparation for transmission?

```
2
```

> Q: Which layer transmits and receives data?

```
1
```

> Q: Which layer encrypts, compresses, or otherwise transforms the initial data to give it a standardised format?

```
6
```

> Q: Which layer tracks communications between the host and receiving computers?

```
5
```

> Q: Which layer accepts communication requests from applications?

```
7
```

> Q: Which layer handles logical addressing?

```
3
```

> Q: When sending data over TCP, what would you call the "bite-sized" pieces of data?

```
segments
```

> Q: **[Research]** Which layer would the FTP protocol communicate with?

```
7
```

> Q: Which transport layer protocol would be best suited to transmit a live video?

```
UDP
```

---

## Task 3 - Encapsulation

As data is passed down each layer the information specific to each is added as a header to the start of the transmission. The data link layer (2) also adds a trailer to the end of the transmission. This is all called **encapsulation**; the process by which data can be sent from one computer to another.

The encapsulated data gets a different name depending on the layer. 

- 7 : Data

- 6 : Data

- 5 : Data

- 4 : Segments / Datagrams

- 3 : Packets

- 2 : Frames

- 1 : Bits

> Q: How would you refer to data at layer 2 of the encapsulation process (with the OSI model)?

```
Frames
```

> Q: How would you refer to data at layer 4 of the encapsulation process (with the OSI model), if the UDP protocol has been selected?

```
Datagrams
```

> Q: What process would a computer perform on a received message?

```
De-encapsulation
```

> Q: Which is the only layer of the OSI model to add a *trailer* during encapsulation?

```
Data Link
```

> Q: Does encapsulation provide an extra layer of security (Aye/Nay)?

```
Aye
```

---

## Task 4 - The TCP/IP Model

A slightly older model than the OSI model that consists of 4 layers that make up the same functions. (Some split 1 into data link and physical but this is the defined standard.)

- **4 - Application**
  
  - Would be layers 7, 6, and 5 of the OSI model.

- **3 - Transport**
  
  - Layer 4 of the OSI model

- **2 - Internet**
  
  - Layer 3 of the OSI model

- **1 - Network Interface**
  
  - Layers 2 and 1 of the OSI model

> We're actually talking about a suite of protocols -- sets of rules that define how an action is to be carried out.

The TCP/IP model is named based on two important protocols. 

TCP is connection based as mentioned before. To send data you must have a stable connection. 

To do that the protocol uses a process called the *three-way handshake*. 

This is the proccess of sending special requests indicate a connection is desired, an acknowledgment of the request with the request, then an acknowledgment that the connection was successful.

- **SYN** - Synchronize packet - The first packet.

- **SYN/ACK** - The synchronize packet with an acknowledgement that is was recieved.

- **ACK** - The acknowledgment on it's own indicated the connection was successful.

> Q: Which model was introduced first, OSI or TCP/IP?

```
TCP/IP
```

> Q: Which layer of the TCP/IP model covers the functionality of the Transport layer of the OSI model **(Full Name)**?

```
Transport
```

> Q: Which layer of the TCP/IP model covers the functionality of the Session layer of the OSI model **(Full Name)**?

```
Application
```

> Q: The Network Interface layer of the TCP/IP model covers the functionality
>  of two layers in the OSI model. These layers are Data Link, and?.. **(Full Name)**?

```
Physical
```

> Q: Which layer of the TCP/IP model handles the functionality of the OSI network layer?

```
Internet
```

> Q: What kind of protocol is TCP?

```
Connection-based
```

> Q: What is SYN short for? (Wants british spelling but no thank you THM :))

```
Synchronize
```

> Q: What is the second step of the three way handshake?

```
SYN/ACK
```

> Q: What is the short name for the "Acknowledgement" segment in the three-way handshake?

```
ACK
```

---

## Task 5 - [Networking Tools] Ping  ([[ping]])

> For the rest of the room we're going to be taking a look at some of the
>  command line networking tools that we can use in practical 
> applications.

What is ping and what do we use it for?

> The ping command is used when we want to test whether a connection to a 
> remote resource is possible. Usually this will be a website on the 
> internet, but it could also be for a computer on your home network if 
> you want to check if it's configured correctly. Ping works using the 
> ICMP protocol, which is one of the slightly less well-known TCP/IP 
> protocols that were mentioned earlier. The ICMP protocol works on the 
> Network layer of the OSI Model, and thus the Internet layer of the 
> TCP/IP model.

Ping is used with the syntax ```ping domain.com``` and returns the IP that the domain is hosted on as well as information about packets sent and if they are recieved.

> Q: What command would you use to ping the bbc.co.uk website?

```shell
ping bbc.co.uk
```

> Q: Ping *muirlandoracle.co.uk*.  What is the IPv4 address?

By default ```ping muirlandoracle.co.uk``` return the IPv6 address. We need to run ```ping domain.com -4``` to force it to return the IPv4 address.

```shell
217.160.0.152
```

> Q: What switch lets you change the interval of sent ping requests?

```
-i
```

> Q: What switch would allow you to restrict requests to IPv4?

```
-4
```

> Q: What switch would give you a more verbose output?

```
-v
```

---

## Task 6 - [Networking Tools] Traceroute

> The logical follow-up to the ping command is 'traceroute'. Traceroute 
> can be used to map the path your request takes as it heads to the target
>  machine.

The basic syntax for traceroute on Linux is ```traceroute <destination>```.

> By default, the Windows traceroute utility (`tracert`) operates using the same ICMP protocol that ping utilises, and the Unix equivalent operates over UDP. This can be altered with switches in both instances.

```shell
 ╭─michaelj@MJ in ~ took 1m32s
 ╰─λ traceroute tryhackme.com
traceroute to tryhackme.com (104.22.54.228), 30 hops max, 60 byte packets
 1  _gateway (192.168.1.1)  3.022 ms  3.006 ms  2.999 ms
 2  142-254-208-233.inf.spectrum.com (142.254.208.233)  30.491 ms  30.485 ms  30.479 ms
 3  lag-63.elwome2202h.netops.charter.com (24.58.225.101)  21.453 ms  21.447 ms  22.628 ms
 4  lag-20.nwptme0504r.netops.charter.com (24.58.50.144)  36.401 ms  37.420 ms  37.412 ms
 5  lag-62.sebgme0302r.netops.charter.com (24.58.50.140)  30.433 ms  30.428 ms  28.337 ms
 6  lag-25.rcr01rochnyei.netops.charter.com (24.58.32.68)  39.338 ms  33.977 ms  38.991 ms
 7  lag-415.chcgildt87w-bcr00.netops.charter.com (66.109.6.2)  52.019 ms  51.936 ms  51.928 ms
 8  lag-0.pr2.chi10.netops.charter.com (66.109.5.225)  50.798 ms lag-301.pr2.chi10.netops.charter.com (209.18.43.61)  49.032 ms  51.525 ms
 9  0.ae4.pr1.dca10.tbone.rr.com (66.109.1.113)  77.611 ms  58.600 ms  77.601 ms
10  141.101.73.22 (141.101.73.22)  58.530 ms 172.70.176.4 (172.70.176.4)  54.223 ms  54.208 ms
11  104.22.54.228 (104.22.54.228)  54.219 ms  54.195 ms  54.190 ms
```

> Q: What switch would you use to specify an interface when using Traceroute?

```
-i
```

> Q: What switch would you use if you wanted to use TCP SYN requests when tracing the route?

```
-T
```

> Q: **[Lateral Thinking]** Which layer of the ***TCP/IP*** model will traceroute run on by default (Windows)?

```
Internet
```

---

## Task 7 - [Networking Tools] WHOIS

Domain name servers serve to link human readable web domains to IP addresses that correspond with servers to allow data transfers around the web. 

Domains are leased to individuals or companies through *domain registrars*.

Whois is a tool that allows you to see who a particular domain is registered to and can sometimes provide a lot of information.

```shell
 ╭─michaelj@MJ in ~ took 462ms
 ╰─λ whois facebook.com
   Domain Name: FACEBOOK.COM
   Registry Domain ID: 2320948_DOMAIN_COM-VRSN
   Registrar WHOIS Server: whois.registrarsafe.com
   Registrar URL: http://www.registrarsafe.com
   Updated Date: 2022-01-26T16:45:06Z
   Creation Date: 1997-03-29T05:00:00Z
   Registry Expiry Date: 2031-03-30T04:00:00Z
   Registrar: RegistrarSafe, LLC
   Registrar IANA ID: 3237
   Registrar Abuse Contact Email: abusecomplaints@registrarsafe.com
   Registrar Abuse Contact Phone: +1-650-308-7004
   Domain Status: clientDeleteProhibited https://icann.org/epp#clientDeleteProhibited
   Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited
   Domain Status: clientUpdateProhibited https://icann.org/epp#clientUpdateProhibited
   Domain Status: serverDeleteProhibited https://icann.org/epp#serverDeleteProhibited
   Domain Status: serverTransferProhibited https://icann.org/epp#serverTransferProhibited
   Domain Status: serverUpdateProhibited https://icann.org/epp#serverUpdateProhibited
   Name Server: A.NS.FACEBOOK.COM
   Name Server: B.NS.FACEBOOK.COM
   Name Server: C.NS.FACEBOOK.COM
   Name Server: D.NS.FACEBOOK.COM
   DNSSEC: unsigned
   URL of the ICANN Whois Inaccuracy Complaint Form: https://www.icann.org/wicf/
>>> Last update of whois database: 2022-06-02T02:13:07Z <<<

For more information on Whois status codes, please visit https://icann.org/epp

The Registry database contains ONLY .COM, .NET, .EDU domains and
Registrars.
Domain Name: FACEBOOK.COM
Registry Domain ID: 2320948_DOMAIN_COM-VRSN
Registrar WHOIS Server: whois.registrarsafe.com
Registrar URL: https://www.registrarsafe.com
Updated Date: 2022-01-26T16:45:06Z
Creation Date: 1997-03-29T05:00:00Z
Registrar Registration Expiration Date: 2031-03-30T04:00:00Z
Registrar: RegistrarSafe, LLC
Registrar IANA ID: 3237
Registrar Abuse Contact Email: abusecomplaints@registrarsafe.com
Registrar Abuse Contact Phone: +1.6503087004
Domain Status: serverUpdateProhibited https://www.icann.org/epp#serverUpdateProhibited
Domain Status: clientDeleteProhibited https://www.icann.org/epp#clientDeleteProhibited
Domain Status: clientTransferProhibited https://www.icann.org/epp#clientTransferProhibited
Domain Status: serverDeleteProhibited https://www.icann.org/epp#serverDeleteProhibited
Domain Status: serverTransferProhibited https://www.icann.org/epp#serverTransferProhibited
Domain Status: clientUpdateProhibited https://www.icann.org/epp#clientUpdateProhibited
Registry Registrant ID: 
Registrant Name: Domain Admin
Registrant Organization: Meta Platforms, Inc.
Registrant Street: 1601 Willow Rd 
Registrant City: Menlo Park
Registrant State/Province: CA
Registrant Postal Code: 94025
Registrant Country: US
Registrant Phone: +1.6505434800
Registrant Phone Ext:
Registrant Fax: 
Registrant Fax Ext:
Registrant Email: domain@fb.com
Registry Admin ID: 
Admin Name: Domain Admin
Admin Organization: Meta Platforms, Inc.
Admin Street: 1601 Willow Rd 
Admin City: Menlo Park
Admin State/Province: CA
Admin Postal Code: 94025
Admin Country: US
Admin Phone: +1.6505434800
Admin Phone Ext:
Admin Fax: 
Admin Fax Ext:
Admin Email: domain@fb.com
Registry Tech ID: 
Tech Name: Domain Admin
Tech Organization: Meta Platforms, Inc.
Tech Street: 1601 Willow Rd 
Tech City: Menlo Park
Tech State/Province: CA
Tech Postal Code: 94025
Tech Country: US
Tech Phone: +1.6505434800
Tech Phone Ext:
Tech Fax: 
Tech Fax Ext:
Tech Email: domain@fb.com
Name Server: C.NS.FACEBOOK.COM
Name Server: B.NS.FACEBOOK.COM
Name Server: A.NS.FACEBOOK.COM
Name Server: D.NS.FACEBOOK.COM
DNSSEC: unsigned
URL of the ICANN WHOIS Data Problem Reporting System: http://wdprs.internic.net/
>>> Last update of WHOIS database: 2022-06-02T02:13:27Z <<<
```

> Q: What is the registrant postal code for facebook.com?

```
94025
```

> Q: When was the facebook.com domain first registered (Format: DD/MM/YYYY)?

```
29/03/1997
```

Performa a whois search on ```microsoft.com```

```shell
 ╭─michaelj@MJ in ~ took 424ms
 ╰─λ whois microsoft.com
   Domain Name: MICROSOFT.COM
   Registry Domain ID: 2724960_DOMAIN_COM-VRSN
   Registrar WHOIS Server: whois.markmonitor.com
   Registrar URL: http://www.markmonitor.com
   Updated Date: 2022-04-18T19:31:04Z
   Creation Date: 1991-05-02T04:00:00Z
   Registry Expiry Date: 2023-05-03T04:00:00Z
   Registrar: MarkMonitor Inc.
   Registrar IANA ID: 292
   Registrar Abuse Contact Email: abusecomplaints@markmonitor.com
   Registrar Abuse Contact Phone: +1.2086851750
   Domain Status: clientDeleteProhibited https://icann.org/epp#clientDeleteProhibited
   Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited
   Domain Status: clientUpdateProhibited https://icann.org/epp#clientUpdateProhibited
   Domain Status: serverDeleteProhibited https://icann.org/epp#serverDeleteProhibited
   Domain Status: serverTransferProhibited https://icann.org/epp#serverTransferProhibited
   Domain Status: serverUpdateProhibited https://icann.org/epp#serverUpdateProhibited
   Name Server: NS1-39.AZURE-DNS.COM
   Name Server: NS2-39.AZURE-DNS.NET
   Name Server: NS3-39.AZURE-DNS.ORG
   Name Server: NS4-39.AZURE-DNS.INFO
   DNSSEC: unsigned
   URL of the ICANN Whois Inaccuracy Complaint Form: https://www.icann.org/wicf/
>>> Last update of whois database: 2022-06-02T02:20:26Z <<<

For more information on Whois status codes, please visit https://icann.org/epp

The Registry database contains ONLY .COM, .NET, .EDU domains and
Registrars.
Domain Name: microsoft.com
Registry Domain ID: 2724960_DOMAIN_COM-VRSN
Registrar WHOIS Server: whois.markmonitor.com
Registrar URL: http://www.markmonitor.com
Updated Date: 2022-04-18T19:25:49+0000
Creation Date: 1991-05-02T04:00:00+0000
Registrar Registration Expiration Date: 2023-05-03T00:00:00+0000
Registrar: MarkMonitor, Inc.
Registrar IANA ID: 292
Registrar Abuse Contact Email: abusecomplaints@markmonitor.com
Registrar Abuse Contact Phone: +1.2086851750
Domain Status: clientUpdateProhibited (https://www.icann.org/epp#clientUpdateProhibited)
Domain Status: clientTransferProhibited (https://www.icann.org/epp#clientTransferProhibited)
Domain Status: clientDeleteProhibited (https://www.icann.org/epp#clientDeleteProhibited)
Domain Status: serverUpdateProhibited (https://www.icann.org/epp#serverUpdateProhibited)
Domain Status: serverTransferProhibited (https://www.icann.org/epp#serverTransferProhibited)
Domain Status: serverDeleteProhibited (https://www.icann.org/epp#serverDeleteProhibited)
Registry Registrant ID: 
Registrant Name: Domain Administrator
Registrant Organization: Microsoft Corporation
Registrant Street: One Microsoft Way, 
Registrant City: Redmond
Registrant State/Province: WA
Registrant Postal Code: 98052
Registrant Country: US
Registrant Phone: +1.4258828080
Registrant Phone Ext: 
Registrant Fax: +1.4259367329
Registrant Fax Ext: 
Registrant Email: admin@domains.microsoft
Registry Admin ID: 
Admin Name: Domain Administrator
Admin Organization: Microsoft Corporation
Admin Street: One Microsoft Way, 
Admin City: Redmond
Admin State/Province: WA
Admin Postal Code: 98052
Admin Country: US
Admin Phone: +1.4258828080
Admin Phone Ext: 
Admin Fax: +1.4259367329
Admin Fax Ext: 
Admin Email: admin@domains.microsoft
Registry Tech ID: 
Tech Name: MSN Hostmaster
Tech Organization: Microsoft Corporation
Tech Street: One Microsoft Way, 
Tech City: Redmond
Tech State/Province: WA
Tech Postal Code: 98052
Tech Country: US
Tech Phone: +1.4258828080
Tech Phone Ext: 
Tech Fax: +1.4259367329
Tech Fax Ext: 
Tech Email: msnhst@microsoft.com
Name Server: ns3-39.azure-dns.org
Name Server: ns4-39.azure-dns.info
Name Server: ns1-39.azure-dns.com
Name Server: ns2-39.azure-dns.net
DNSSEC: unsigned
URL of the ICANN WHOIS Data Problem Reporting System: http://wdprs.internic.net/
>>> Last update of WHOIS database: 2022-06-02T02:16:09+0000 <<<
```

> Q: Which city is the registrant based in?

```
Redmond
```

> Q: **[OSINT]** What is the name of the golf course that is near the registrant address for microsoft.com?

```
Bellevue Golf Course
```

> Q: What is the registered Tech Email for microsoft.com?

```
msnhst@microsoft.com
```

---

## Task 8 - [Networking Tools] Dig

> Ever wondered how a URL gets converted into an IP address that 
> your computer can understand? The answer is a TCP/IP protocol called DNS (**D**omain **N**ame **S**ystem).

> Before 2004 there were precisely 13 root name DNS servers in the world. These days there are many more; however, they are still accessible using the same 13 IP addresses assigned to the original servers (balanced so that you get the closest server when you make a request). The root name servers essentially keep track of the DNS servers in the next level down, choosing an appropriate one to redirect your request to. These lower level servers are called *Top-Level* *Domain* servers.
> 
> Top-Level Domain (TLD) servers are split up into extensions. So, for example, if you were searching for tryhackme**.com** your request would be redirected to a TLD server that handled `.com` domains. If you were searching for bbc**.co.uk** your request would be redirected to a TLD server that handles `.co.uk` domains. As with root name servers, TLD servers keep track of the next level down: *Authoritative name servers*. 
> 
> When a TLD server receives your request for information, the server 
> passes it down to an appropriate Authoritative name server.
> 
> Authoritative name servers are used to store DNS records for domains directly. In other words, every domain in the world will have its DNS records stored on an Authoritative name server somewhere or another; they are the source of the information. When your 
> request reaches the authoritative name server for the domain you're querying, it will send the relevant information back to you, allowing your computer to connect to the IP address behind the domain you requested.

This all automatically happens when we visit website, but with dig we can do it manually. 

Dig lets us query recursive DNS servers for information about domains.

Example:

```shell
 ╭─michaelj@MJ in ~ took 982ms
 ╰─λ dig google.com @1.1.1.1

; <<>> DiG 9.18.3 <<>> google.com @1.1.1.1
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 35235
;; flags: qr rd ra; QUERY: 1, ANSWER: 6, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;google.com.                    IN      A

;; ANSWER SECTION:
google.com.             280     IN      A       172.253.115.101
google.com.             280     IN      A       172.253.115.138
google.com.             280     IN      A       172.253.115.139
google.com.             280     IN      A       172.253.115.102
google.com.             280     IN      A       172.253.115.100
google.com.             280     IN      A       172.253.115.113

;; Query time: 60 msec
;; SERVER: 1.1.1.1#53(1.1.1.1) (UDP)
;; WHEN: Thu Jun 02 00:04:30 EDT 2022
;; MSG SIZE  rcvd: 135
```

> Q: What is DNS short for?

```
Domain Name System
```

> Q: What is the first type of DNS server your computer would query when you search for a domain?

```
Recursive
```

> Q: What type of DNS server contains records specific to domain extensions (i.e. *.com,* .co.uk*, etc)*? Use the long version of the name.

```
Top-Level Domain
```

> Q: Where is the very first place your computer would look to find the IP address of a domain?

```
Local Cache
```

> Q: **[Research]** Google runs two public DNS servers. One of them can be queried with the IP 8.8.8.8, what is the IP address of the other one?

```
8.8.4.4
```

> Q: If a DNS query has a TTL of 24 hours, what number would the dig query show?

```
86400
```

---

## Task 9 - Further Reading

> In terms of further information, feel free to reach out in the TryHackMe Discord if you want any help with the contents of this room. 
> Additionally, if you want to expand your knowledge of networking theory, the [CISCO Self Study Guide by Steve McQuerry](https://www.amazon.co.uk/Interconnecting-Cisco-Network-Devices-ICND1/dp/1587054620/ref=sr_1_1?keywords=Interconnecting+Cisco+Network+Devices%2C+Part+1&qid=1583683766&sr=8-1) is a great resource to work from. 
> 
> There may be a more up to date version available; however, this edition is cheap, readily available, and most importantly, still very relevant. 
> 
> Whilst it is designed to as a study guide for the CCNA exam, that book serves equally well as a very rounded introduction to networking principles.

---
[[THM-Introductory-Networking]]
[[Networking-Refresher]]

[[THM-Nmap-Live-Host-Discovery]]
[[General Linux/Command Reference Library/nmap]]
[[ping]]
