# Introductory Researching

[TryHackMe | Introductory Researching](https://tryhackme.com/room/introtoresearch)

> Michael Jack | 06/2022

---

## Task 1 - Introduction

> We will be looking at the following topics:  
> 
> • An example of a research question  
> 
> • Vulnerability Searching tools  
> 
> • Linux Manual Pages

---

## Task 2 - Example Research Question

Goes over how to start with a question and build up a picture of what we need to to via an example process of going from "how do I get information out of an image?", to installing stegonography tools and utilizing them.

> Q: In the Burp Suite Program that ships with Kali Linux, what mode would you use to manually send a request (often repeating a captured request numerous times)?

```
repeater
```

> Q: What hash format are modern Windows login passwords stored in?

```
NTLM
```

> Q: What are automatic tasks called in Linux?

```
cron jobs
```

> Q: What number base could you use as shorthnand for base 2 (binary)?

```
base 16
```

> Q: If a password hash starts with \$6\$, what format is it (Unix variant)?

```
SHA512 crypt
```

---

## Task 3 - Vulnerability Searching

> Often in hacking you'll come across software that might be open to 
> exploitation. For example, Content Management Systems (such as 
> Wordpress, FuelCMS, Ghost, etc) are frequently used to make setting up a
>  website easier, and many of these are vulnerable to various attacks. So
>  where would we look if we wanted to exploit specific software?

We can use sites such as:

- https://www.exploit-db.com/

- https://nvd.nist.gov/vuln/search

- https://cve.mitre.org/

> CVEs take the form: CVE-YEAR-IDNUMBER

We can also use tools like searchsploit from the terminal to access ExploitDB or other databases locally.

> Q: What is the CVE for the 2020 XSS vulnerability found is WPForms?

```
CVE-2020-10385
```

> Q: There was a local privesc vulnerability found in the Debian version of Apache Tomcat, back in 2016. What's the CVE for this vulnerability?

```
CVE-2016-1240
```

> What is the very first CVE found in the VLC media player?

```
CVE-2007-0017
```

> If you wanted to exploit a 2020 buffer overflor in the sudo program, which CVE would you use?

```
CVE-2019-18634
```

---

## Task 4 - Manual Pages

> One of the many useful features of Linux is the inbuilt `man` command,
>  which gives you access to the manual pages for most tools directly 
> inside your terminal. Occasionally you'll find a tool that doesn't have a
>  manual entry; however, this is rare. Generally speaking, when you don't
>  know how to use a tool, `man` should be your first port of call.

We canb use man pages to look up switches and flags we can use to change what a command does, and generally better understand how to accomplish what we want with a given tool.

> Q: SCP is a tool used to copy files from one computer to another.  
> *What switch would you use to copy an entire directory?*

```
-r
```

> Q: fdisk is a command used to view and alter the partitioning scheme used on your hard drive.  
> *What switch would you use to list the current partitions?*

```
-l
```

> Q: nano is an easy-to-use text editor for Linux. There are arguably better 
> editors (Vim, being the obvious choice); however, nano is a great one to
>  start with.  
> *What switch would you use to make a backup when opening a file with nano?*

```
-b
```

> Q: Netcat is a basic tool used to manually send and receive network requests.   
> *What **command** would you use to start netcat in listen mode, using port 12345?*

```shell
nc -l -p 12345
```

---

## Task 5 - Final Thoughts

> You may have been told in school that there are good sources and bad sources of information. That may be true when it comes to essays and referencing information; however, it's my pleasure to state that it does not apply here. Any information can 
> potentially be useful -- so feel free to use blogs, wikipedia, or anything else that contains what you're looking for! Blogs especially can often be very valuable for learning when it comes to information security, as many security researchers keep a blog.
> 
> Having completed this room, you hopefully now have established the basis of a methodology to tackle research questions that you come across by yourself. The vast majority of rooms on TryHackMe can be solved purely using knowledge found on Google, so please take the opportunity to improve your skills by Googling any problems you come across!

As a follow-up to this room, complete CMNatic's [Google Dorking](https://tryhackme.com/room/googledorking) room to learn some advanced Google tricks!

---
