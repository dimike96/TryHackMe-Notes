# THM - The Hacker Methodology

[TryHackMe | The Hacker Methodology](https://tryhackme.com/room/hackermethodology)

> Michael Jack | 06/2022

--- 

## Task 1 - What Process Does a Hacker Follow?

> <u><b>The Process that pentesters follow is summarized in the following steps:</b></u>
> 
> 1. **Reconnaissance**
> 2. **Enumeration/Scanning**
> 3. **Gaining Access**
> 4. **Privilege Escalation**
> 5. **Covering Tracks**
> 6. **Reporting**

---

## Task 2 - Reconnaissance Overview

> **It's good to know the following tools:** 
> 
> - **Google (specifically Google Dorking)**
> - **Wikipedia**
> - **PeopleFinder.com**
> - **who.is**
> - **sublist3r**
> - **hunter.io**
> - **builtwith.com**
> - **wappalyzer**

> Q: Who is the CEO of SpaceX?

```
Elon Musk
```

> Q: Do some research intot he tool "sublist3r". What does it list?

```
subdomains
```

> Q: What is it called when you use Google to look for specific vulnerabilities or to research a specific topic of interest?

```
Google Dorking
```

---

## Task 3 - Enumeration and Scanning Overview

After research comes **scanning** and **enumeration**.

> **This is where more specialized tools start to come in to the arsenal.** Tools like nmap, dirb, metasploit, exploit-db, Burp Suite and others 
> are very useful to help us try to find vulnerabilities in a target.

Some useful tools include:

- Nmap

- dirb

- dirbuster

- enum4linux

- metasploit

- burp suite

> Q: What does enumeration help to determine about the targer?

```
attack surface
```

> Q: Do some reconnaissance about the tool "Metasploit", what company developed it?

```
Rapid7
```

> Q: What company developed the tech behind the tool Burp Suite?

```
Portswigger
```

---

## Task 4 - Exploitation

Now that we have done research and exposed potential attack surfaces and vulnerabilities this is where that information is put to use.

Using tools like Metasploit, msfvenom, Burp, SQLMap, etc., the vulnerabilities are taken advantage of.

> Q: What is one of the primary exploitation tools that pentesters use?

```
Metasploit
```

---

## Task 5 - Privilege Escalation (Privesc)

Usually when access is gained it isn't complete access to everything we need. For example, we may be on an user account but not an administrator account, or we don't have sudo privileges, etc..

> **Privilege escalation can take many, many forms, some examples are:**
> 
> - Cracking password hashes found on the target
> - Finding a vulnerable service or version of a service which will allow you to escalate privilege THROUGH the service
> - Password spraying of previously discovered credentials (password re-use)
> - Using default credentials
> - Finding secret keys or SSH keys stored on a device which will allow pivoting to another machine
> - Running scripts or commands to enumerate system settings like 'ifconfig' to find network settings, or the command 'find / -perm  
>   -4000 -type f 2>/dev/null' to see if the user has access to any commands they can run as root

Privesc can take a variety of forms. This would include pivoting to another machine, or getting higher access all with the goal to "own" or "pwn" a machine.

> Q: In Windows what is the common target account besides Admin?

```
System
```

> What thing related to SSH could let you login to another machine without credentials (username & passwd?

```
keys
```

---

## Task 6 - Covering Tracks

> Most professional/ethical penetration testers never have the need to "cover 
> their tracks". However, this is still a phase in the methodology.
> 
> You should always have explicit permission from the system owner regarding 
> when the test is happening, how its occurring, and the scope of targets 
> in any penetration test.
> 
> **Since the rules of engagement for a penetration test should be agreed to before the test occurs, the penetration tester should stop IMMEDIATELY when they have achieved 
> privilege escalation and report the finding to the client.** 
> 
> As such, a professional will never cover their tracks because the assessment was planned to and agreed to beforehand. Although there are multiple tools for covering tracks, I will not talk about any of them in this room. If you are truly curious you may research them yourself.
> 
> However, even though you do not cover your tracks, this does not resolve you of 
> liability for your exploitation. Often you will need to assist the IT Administrator or system owner in cleaning up the exploit code that you utilized, and also recommending HOW to prevent the attack in the future.
> 
> **While ethical hackers rarely have a need to cover their tracks, you still must carefully track and notate all of the tasks that you performed as part of the penetration test to assist in fixing the vulnerabilities and recommending changes to the system owner.**

When it comes to ethical hacking, pentesting, etc. (red team) you don't really cover your tracks, but you need to know what tracks you leave as it is extremely helpful for the more "blue team" side of things where systems are hardened and exploits are patched or protected against. 

---

## Task 7 - Reporting

> This is one of the most important phases where you will outline everything that you found. **The reporting phase often includes the following things:**
> 
> - **The Finding(s) or Vulnerabilities**
> - **The CRITICALITY of the Finding**
> - **A description or brief overview of how the finding was discovered**
> - **Remediation recommendations to resolve the finding**

A full formal report sample can be found here: [GitHub - hmaverickadams/TCM-Security-Sample-Pentest-Report: Sample pentest report provided by TCM Security](https://github.com/hmaverickadams/TCM-Security-Sample-Pentest-Report).

> *The CyberMentor has a lot of other good content such as example resumes, YouTube videos, and some really good Udemy courses (http://udemy.com/course/practical-ethical-hacking/) that will take you beyond the basics of this methodology outline.*

Generally reports include such information as:

- Finding
  
  - What was found? What vulnerability?

- Criticality
  
  - How severe, or disruptive is this? How serious is the risk?

- Description
  
  - More detail

- Remediation
  
  - How can it be prevented, fixed, resolved, patched, etc..

> Q: What would be the type of reporting that involves a full documentation of all finding within a formal document?

```
full formal report
```

> Q: What is the other thing that a pentester should provide in a report 
> beyond: the finding name, the finding description, the finding 
> criticality?

```
Remediation Recommendation
```

---


