# THM Intro to Offensive Security

[TryHackMe | Intro to Offensive Security](https://tryhackme.com/room/introtooffensivesecurity)

> Michael Jack | 06/2022

---

## Task 1 - Hacking your first machine

We will get access to a fake bank application called "FakeBank".

> We will use a command-line application called "GoBuster" to brute-force FakeBank's website to find hidden directories and pages. 
> GoBuster will take a list of potential page or directory names and tries accessing a website with each of them; if the page exists, it tells you.

```http://10.10.48.31/```

We can use tools like Gobuster, Dirbuster, Feroxbuster, or other varients to brute-force possible directories and pages available on a website.

*Note: Dirbuster wordlists reside at ```/usr/share/dirbuster```*

(*This is the one I've used most: ```/usr/share/dirbuster/directory-list-lowercase-2.3-medium.txt```*)

The challenge says that running the command:
```shell
gobuster -u http://fakebank.com -w wordlist.txt dir
```
Will find some ```/bank-transfer```. Those flags didn't work with gobuster and ```wordlist.txt``` doesn't really specify the wordlist to use.

Due to this I just ran a normal dirbuster scan and found a ```/js/script.js``` file.

In there was a function "showWinningMsg":
```js
function showWinningMsg() {
  const winMsgEl = document.querySelector('#winning-msg')
  winMsgEl.innerHTML = `<div class='winning-msg d-flex align-items-center'>
    <div class='winning-emoji'>
      🎉
    </div>
    <div>
      <div>Congratulations - you hacked the bank!</div>
      <div>The answer to the TryHackMe question is <b>BANK-HACKED</b></div>
    </div>
  </div>`
  addWinningTransaction()
}
```

### Questions

> When you've transferred money to your account, go back to your bank account page. What is the answer shown on your bank balance page?

```
BANK-HACKED
```

>  If you were a penetration tester or security consultant, this is an exercise you’d perform for companies to test for vulnerabilities in their web applications; find hidden pages to investigate for vulnerabilities.

---

## Task 2 - What is Offensive Security?

> In short, offensive security is the process of breaking into computer systems, exploiting software bugs, and finding loopholes in applications to gain unauthorized access to them.

Essentially testing systems, software, networks, etc. from the perspective of an attacker to find and repair vulnerabilities.

Compared to defensive security that is dedicated to protecting networks and systems from similar real malicious threats.

---

## Task 3 - Careers in Cyber Security

How can one get into a job as an ethical hacker or a security analyst, or cybersecurity in general?

> Break it down, learn an area of cyber security you're interested in, and regularly practice using hands-on exercises. Build a habit of learning a little bit each day

What careers are there?

The cyber careers room goes into more depth about the different careers in cyber. However, here is a short description of a few offensive security roles:

-   Penetration Tester - Responsible for testing technology products for finding exploitable security vulnerabilities.
-   Red Teamer - Plays the role of an adversary, attacking an organization and providing feedback from an enemy's perspective.
-   Security Engineer - Design, monitor, and maintain security controls, networks, and systems to help prevent cyberattacks.

---
