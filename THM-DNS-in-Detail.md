# THM - DNS in Detail

[TryHackMe | DNS in Detail](https://tryhackme.com/room/dnsindetail)

> Michael Jack | 06/2022

---

## Task 1 - What is DNS?

**DNS** (Domain Name System) allows for easy communication between devices on the internet without remembering IP addresses 

*Recall: An IP address looks like the following 104.26.10.229, 4 sets of digits ranging from 0 - 255 separated by a period.*

DNS maps human readable domains to network IP addresses so that we can navigate the web easily.

### Questions

> What does DNS stand for?

```
Domain Name System
```

---

## Task 2 - Domain Hierarchy

We can split domains up into levels that make up a hierarchy. 

### Top-Level Domain (TLD)

A top level domain is the rightmost part of the domain. The ".com", ".org", ".net", etc.. 

Top level domains further can be split into generic top-level domains (gTLD) and country code top-level domains (ccTLD). This is the difference between ".com" and say, ".ca", or ".co.uk".

[Full List of Top-Level Domains](https://data.iana.org/TLD/tlds-alpha-by-domain.txt)

### Second-Level Domains

The second-level domain is the part generally recognized as the websites name. More accurately, the part that comes immediately before the top-level domain.

With the example "tryhackme.com" the second-level domain is the "tryhackme".

> When registering a domain name, the second-level domain is limited to 63 characters + the TLD and can only use a-z 0-9 and hyphens (cannot start or end with hyphens or have consecutive hyphens).

### Subdomain

There isn't always a subdomain but this would be on the left of the second-level domain. 

If we had an example like "admin.tryhackme.com" the subdomain is the "admin" part.

> A subdomain name has the same creation restrictions as a Second-Level Domain, being limited to 63 characters and can only use a-z 0-9 and hyphens (cannot start or end with hyphens or have consecutive hyphens).

However, there is not limit to the number of subdomains you can have, as long as the length is less or equal to 253 characters. 

### Questions

> What is the maximum length of a subdomain?

```
63
```

> Which of the following characters cannot be used in a subdomain ( 3 b _ - )?

```
_
```

> What is the maximum length of a domain name?

```
253
```

> What type of TLD is .co.uk?

```
ccTLD
```

---

## Task 3 - Record Types

> DNS isn't just for websites though, and multiple types of DNS record exist. We'll go over some of the most common ones that you're likely to come across.

### Some Common DNS Record Types

**A Record**: These records resolve to IPv4 addresses

**AAAA Record**: These records resolve IPv^ addresses

**CNAME Record**: These records resolve to another domain name. For example a website having a subdomain that redirects to their shop somewhere like Shopify.

**MX (Mail Exchange) Record**: These records resolve to the address of the servers that handle the email for the domain you are querying. 
The MX record indicates how email messages should be routed in accordance with the SMTP.

**TXT Record**: These records are free text fields where any text data can be stored. 
They have multiple uses, but some common ones can be to list servers that have the authority to send an email on behalf of the domain (this can help in the battle against spam and spoofed email). 
They can also be used to verify ownership of the domain name when signing up for third party services.

### Questions

> What type of record would be used to advise where to send email?

```
MX
```

> What type of record handles IPv6 addresses?

```
AAAA
```

---

## Task 4 - Making a Request


### What happens when you make a DNS request?

1. Computer checks its local cache to see if it has the address from a recent lookup. If not then it sends a request to your *Recursive DNS Server*.
2. A Recursive DNS Server is usually provided by your ISP, but you can also choose your own. This server also has a local cache of recently looked up domain names. If a result is found locally, this is sent back to your computer, and your request ends here (this is common for popular and heavily requested services). If the request cannot be found locally, a journey begins to find the correct answer, starting with the internet's root DNS servers.
3. The root servers act as the DNS backbone of the internet; their job is to redirect you to the correct Top Level Domain Server, depending on your request. If, for example, you request [www.tryhackme.com](http://www.tryhackme.com/), the root server will recognise the Top Level Domain of .com and refer you to the correct TLD server that deals with .com addresses.
4. The TLD server holds records for where to find the authoritative server to answer the DNS request. The authoritative server is often also known as the nameserver for the domain. For example, the name server for [tryhackme.com](http://tryhackme.com) is [kip.ns.cloudflare.com](http://kip.ns.cloudflare.com) and [uma.ns.cloudflare.com](http://uma.ns.cloudflare.com). You'll often find multiple nameservers for a domain name to act as a backup in case one goes down.
5. An authoritative DNS server is the server that is responsible for storing the DNS records for a particular domain name and where any updates to your domain name DNS records would be made. Depending on the record type, the DNS record is then sent back to the Recursive DNS Server, where a local copy will be cached for future requests and then relayed back to the original client that made the request. DNS records all come with a TTL (Time To Live) value. This value is a number represented in seconds that the response should be saved for locally until you have to look it up again. Caching saves on having to make a DNS request every time you communicate with a server.

### Questions

> What field specifies how long a DNS record should be cached for?

```
TTL
```

> What type of DNS Server is usually provided by your ISP?

```
Recursive
```

> What type of server holds all the records for a domain?

```
Authoritative
```

---

## Task 5 - Practical

### Questions

> What is the CNAME of shop.website.thm?

```
shops.myshopify.com
```

> What is the value of the TXT record of website.thm?

```
THM{7012BBA60997F35A9516C2E16D2944FF}
```

> What is the numerical priority value for the MX record?

```
30
```

> What is the IP address for the A record of www.website.thm?

```
10.10.10.10
```

---
