# THM - Vulnerabilities 101

[TryHackMe | Vulnerabilities 101](https://tryhackme.com/room/vulnerabilities101)

> Michael Jack | 06/2022

---

## Task 1 - Introductions

> This room is going to introduce you to some resources that are essential when researching vulnerabilities, specifically, you are going to be introduced to:
> -   What vulnerabilities are
> -   Why they're worthy of learning about
> -   How are vulnerabilities rated
> -   Databases for vulnerability research
> -   A showcase of how vulnerability research is used on ACKme's engagement

---

## Task 2 - Introduction to Vulnerabilities

> A **vulnerability** in cybersecurity is defined as a weakness or flaw in the design, implementation or behaviours of a system or application.
> NIST defines a vulnerability as “weakness in an information system, system security procedures, internal controls, or implementation that could be exploited or triggered by a threat source”.

Vulnerabilities can be grouped into categories.

- Operating System
	- Found within OSs and often lead to privesc.
- (Mis)Configuration-Based
	- Resulting from incorrect or insecurely configured applications, devices, services. 
- Weak or Default Credentials
	- Vulnerable credentials that are known defaults or insecure to password attacks.
- Application Logic
	- Resulting from poorly designed applications. For example poorly implemented authentication methods.
- Human-Factor
	- Leverages human behavior. I.e social engineering and such.

### Questions

> An attacker has been able to upgrade the permissions of their system account from "user" to "administrator". What type of vulnerability is this?

```
Operating System
```

> You manage to bypass a login panel using cookies to authenticate. What type of vulnerability is this?

```
Application Logic
```

---

## Task 3 - Scoring Vulnerabilities (CVSS & VPR)

>Vulnerability management is the process of evaluating, categorising and ultimately remediating threats (vulnerabilities) faced by an organisation.

The goal is to manage and mitigate risks as they can't be completely eliminated.

Given this theres value in scoring the severity of vulnerabilities to focus attention and resources for the greatest effect.

### Common Vulnerability Scoring System (CVSS)

The CVSS was introduces in 2005 and has gone through several revisions.

It ranks vulnerabilities based on a large number of different factors such as:

- How easy is it to exploit the vulnerability?
- Do exploits exist?
- How does the vulnerability interfere with the CIA triad?

[Here](https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator) is a calculator to score a vulnerability based on the CVSS.

It produces a score that can be places into a Qualitative Severity Rating Scale that goes from None, to Low, to Medium, to High, and to Critical as the highest severity class.

There are advantages as this framework has been around a long time, is popular among organizations, and is free to adopt and recommended by groups like NIST.

However it's also not meant to prioritize vulnerabilities, just assign severity values. 

It also puts an emphasis on vulnerabilities that have exploits available but only about 20% of vulnerabilities do.

It also doesn't adapt to new developments such as exploit releases. A vulnerabilities score is more or less static.

### Vulnerability Priority Rating (VPR)

> The VPR framework is a much more modern framework in vulnerability management - developed by Tenable, an industry solutions provider for vulnerability management.
> This framework is considered to be risk-driven; meaning that vulnerabilities are given a score with a heavy focus on the risk a vulnerability poses to the organisation itself, rather than factors such as impact (like with CVSS).

VPR makes into account relevence of vulnerabilities and is considerably dynamic, where scores can change nearly daily.

Similarly VPR scores can go from Low, to Medium, to High, and to Critical. Differing from CVSS in that it lacks an None category.

VPR has advantages in that it's more modern and "real-world", considers many factors, is risk-driven to help organizations prioritize, and has dynamic scoring.

However it's not open-source and can only be adopted commerically, and it doesn't consider the CIA triad.

### Questions

> What year was the first iteration of CVSS published?

```
2005
```

> If you wanted to assess vulnerability based on the risk it poses to an organisation, what framework would you use?

```
VPR
```

> If you wanted to use a framework that was free and open-source, what framework would that be?

```
CVSS
```

---

## Task 4 - Vulnerability Databases

> Thankfully for us, there are resources on the internet that keep track of vulnerabilities for all sorts of software, operating systems and more! 
> This room will showcase two databases that we can use to look up existing vulnerabilities for applications discovered in our infosec journey, specifically the following websites: [NVD](https://nvd.nist.gov/vuln/full-listing) and [Exploit-DB](http://exploit-db.com/).

The National Vulnerability Database lists all publically categorised vulnerabilities.

> While this website helps keep track of new vulnerabilities, it is not great when searching for vulnerabilities for a specific application or scenario.

Eploit-DB has exploits for software and applications that you can find given their names authors or version numbers.

> We can use Exploit-DB to look for snippets of code (known as Proof of Concepts) that are used to exploit a specific vulnerability.

### Questions

> Using [NVD](https://nvd.nist.gov/vuln/full-listing), how many CVEs were submitted in July 2021?

```
1585
```

> Who is the author of [Exploit-DB](https://www.exploit-db.com/)?

```
Offensive Security
```

---

## Task 5 - An Example of Finding a Vulnerability

If we know the service/software we are targeting, and even more so if we know the version of that service/software, we can use that to find potential vulnerabilities and exploits for it.

Being able to garner the version information can be called a "**Version Disclosure**" vulnerability.

Example given of a version disclosure and lookup for an apache tomcat server.

### Questions

> What type of vulnerability did we use to find the name and version of the application in this example?

```
Version Disclosure
```

---

## Task 6 - Showcase: Exploiting Ackme's Application

> It is your first week on the job as Jr. Penetration tester at ThePentestingCo. For your first engagement, you are shadowing a Sr. Penetration Tester within the company.
> Deploy the site attached to this task and follow the steps that the Sr. Penetration Tester took to exploit a vulnerability against ACKme IT Service's infrastructure.
> **Complete the engagement to retrieve a flag.**

```
THM{ACKME_ENGAGEMENT}
```

---

