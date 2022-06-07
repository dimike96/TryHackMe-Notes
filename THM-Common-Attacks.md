# THM - Common Attacks

[TryHackMe | Common Attacks](https://tryhackme.com/room/commonattacks)

> Michael Jack | 06/22

---

## Task 1 - Introduction

Objective:

- Cover common tactics used by attackers against people online.
- Cover some of the best ways to prevent these tactics from being successful.

---

## Task 2 - [Common Attacks] Social Engineering

### What is Social Engineering?

Social engineering is the name given to cyberattacks where a *human* is the targer.

The exploited vulnerability is the human element.

> Social engineering attacks are often multi-layered and escalate due to the snowball effect.

Videos about social engineering:

[Defcon23](https://youtu.be/fHhNWAKw0bY?t=100)
[CNN](https://youtu.be/PWVN3Rq4gzw)

### Other Forms of Social Engineering

Social engineering may present as dropping usb thumb drives around hoping for someone to be curious and plug one in.

It could also be a public charging port with hidden device to tranfer malware to a unsuspecting person using it.

There are countless ways for people to be the target of hacks.

### Staying Safe From Social Engineering Attacks

- Always use MFA and use strong passwords.
	- Consider using "false" security questions.
-Never plug in external media that isn't yours or you aren't sure is safe into any device.
- Always insist for identity verification with strangers claiming to be with any company or authority.
	- Try to communicate over a different trusted method.

### Questions

> What was the original target of Stuxnet?

```
the Iran nuclear programme
```

---

## Task 3 - [Common Attacks] Social Engineering: Phishing

> Phishing is one of the most common cyber attack types employed by scammers and bad actors, targeting individuals and businesses indiscriminately.

Phishing, Spearphishing, and Whaling are all related and similar.

Phishing the most general and least targeting, and whaling being targeted at high profile individuals.

### Identifying Phishing Attacks

- Look out for links with different redirects than they appear to be.
- Look out for excessive speeling or grammar errors.
- Look out for poor, or different than normal formatting or graphics.
- Look for close but not right email addresses, or mispelled domains.

### Questions

> What is the flag?

```
THM{I_CAUGHT_ALL_THE_PHISH}
```

---

## Task 4 - [Common Attacks] Malware and Ransomeware

> Malware (short for "malicious software") can be defined as any software designed to perform malicious actions on behalf of an attacker.

### Rasomware

Malware with the goal of infecting many systems in order to extort a ransom from users or administrators or organizations to be able to access the data the software has encrypted.

Notable example is the Wannacry ransomware that exploited the Eteral Blue exploit MS017-010 to spread rapidly accross networks using a vulnverability in Windows SMB.

### Delivery Methods

There are many ways to deliver malware to a target.

The most common delivery method is through e-mail using phishing methods, or some other social engineering attack.

A Word or Excel file could have malicious macros embedded that could stage even more malicious code, as an example.

Alternatively, the attacker may exploit a vulnerability in public-facing infrastructure in a corporate environment (for example, a webserver). 
Thus giving themselves an opening into the internal network and allowing them to start a larger attack, facilitated by malware.

### Staying Safe

- Keep software and systems up to date - patch quickly always!
- Don't click suspicious links, hover and check always!
- Be on the lookout for trickery, be suspicious!
- Do not plug in unknown devices!!!
- Back up important data! Preferably in different locations / forms.
- Use up to date and active AV products or EDR.

### Questions

> [Research] What currency did the Wannacry attacker request payment in?

```
Bitcoin
```

---

## Task 5 - [Common Attacks] Passwords and Authentication

- Do not reuse passwords
- Use strong passwords - difficult to guess, long strings with random patterns, case changes, special characters, etc. Utilize a password manager and change passwords regularly, especially in the event of a breach.
- Do not use any information about you that other people know or could guess
- Monitor and stay up to date on any breaches with companies you have accounts with or do business with!

### Questions

> What is the password?

```
TryHackMe123!
```

---

## Task 6 - [Staying Safe] MFA and Password Managers

### Multi-Factor Authentication

> **M**ulti-**F**actor **A**uthentication (or MFA) is a term used to describe any authentication process where you need more than one thing to log in.

Common methods are being sent a six digits code through email, an authenticator app, or (*less ideally and less securely*) a sms message.

Three main MFA types:

- Something you *have*
	- Authentication key, or other hardware token
- Something you *know*
	- Password, security question, etc.
- Something you *are*
	- Biometrics

**You should use MFA when it is available!!!**

Do **not** use sms based MFA if you have any other option. Prefer apps like Google Authenticator (my fav) or Authy, etc..

### Password Managers and Generating Strong Passwords

Password managers make it practical to use proprely secure passwords.

They help you generate unique, strong passwords for every site you use and store them securely, encrypted behind a master password, or biometrics. 

My favorite: Bitwarden (*Having used lastpass and 1password before, bitwarden has all the best features for **free** and the option to self host.*)

Article on SMS insecurities: [Can We Stop Pretending SMS is Secure Now?](https://krebsonsecurity.com/2021/03/can-we-stop-pretending-sms-is-secure-now/)

### Questions

> Where you have the option, which should you use as a second authentication factor between SMS based TOTPs or Authenticator App based TOTPs (SMS or App)?

```
App
```

---

## Task 7 - [Staying Safe] Public Network Safety

> The internet plays a _gargantuan_ role in modern life, with most people being connected in some way virtually constantly. 
> As such, most public spaces (e.g. cafés, restaurants, public transport) are fully equipped with public WiFI to let people catch up on email (or, equally likely, play the latest hit mobile game).
> What many people _don't_ realise is that expecting public WiFi to be available can prove to be very dangerous indeed.

With public wifi you can't be sure of who else is on the network (or what devices are) and what they are doing.

Man-in-the-middle attacks happen when someone is able to snoop on traffic while it is transit. 

Since HTTPS is the standard now, and it uses TLS to encrypt traffic the risk is reduced as information is not sent in plain text like with HTTP.

Ideally we avoid connecting to untrusted networks.

If we need to, VPN's are an option to encrypt and redirect traffic. There is nothing that can stop any VPN provider from keeping information on you no matter their claims regarding keeping logs. 

Do not use any VPN provider, host your own if you need to. ([Don't Use VPN Services.](https://gist.github.com/joepie91/5a9909939e6ce7d09e29))

### Website Connection Security

There are protocols and methods in place to help keep you safe online.

The browsers you use should have a padlock icon to indicate that the connection is secure using TLS. This doesn't validate the website but the connection.

Also browsers might warn you about insecure connections if there's a problem with the SSL certificate that verifies who the website is.

There are also safe browsing features to protect you from otherwise malicious websites.

---

## Task 8 - [Staying Safe] Backups

> Backups are arguably the single most important defensive measure you can take to protect your data. 
> No matter what happens, if you have taken appropriate steps to back your information up, you will always be able to recover almost regardless of the severity of the damage.

### The Golden 3,2,1 Rule

- You should always have **3** up to date copies of your data
- Backups should be stores on at least **2** different storage mediums
- **1** (+) backups should be stored off-site. 

### Questions

> What is the minimum number of up-to-date backups you should make?

```
3
```

> Of these, how many (at minimum) should be stored in another location?

```
1
```

---

## Task 9 - [Staying Safe] Updates and Patches

> Updates are an essential part of the software development lifecycle; they allow developers to add new features, fix bugs and otherwise simply alter aspects of the product. 
> When vulnerabilities are discovered in software, the developers usually release special updates called _patches_ that contain a fix for the vulnerability or otherwise "patch" the security issue.

Recall how Eternal Blue ([ms17-010](https://docs.microsoft.com/en-us/security-updates/SecurityBulletins/2017/ms17-010)) was the result of a vulnerability and was late patched with a software update.

Antivirus software also need to be maintained because they rely on an up to date database of malware signatures and indicators of compromise (IoCs).

Essentially: **Update your software and systems!!**

Consider completing the room [Blue](https://tryhackme.com/room/blue) to play with Eternal Blue.

---

## Task 10 - Conclusion

> To conclude: there are many different options for a malicious attacker to target both individuals and sweeping groups; however, there are remediations for every attack.
> Having completed this room, you should hopefully understand a little more about these common attacks and the defences against them. 
> You don't need to be an expert in computers or cybersecurity to stay safe online: the solutions are simple and well-worth adopting in your personal and professional online interactions.

---
