# THM Linux Fundamentals 1
[TryHackMe | Login](https://tryhackme.com/jr/linuxfundamentalspart1)

> Michael Jack | 06/2022

---

## Task 1 - Intro

> Welcome to the first part of the "Linux Fundamentals" room series. You're
>  most likely using a Windows or Mac machine, both are different in 
> visual design and how they operate. Just like Windows, iOS and MacOS, Linux is just another operating system and one of the most popular in the 
> world powering smart cars, android devices, supercomputers, home 
> appliances, enterprise servers, and more.
> 
> We'll be covering some of the history behind Linux and then eventually starting your journey of being a Linux-wizard! This room will have you:
> 
> - Running your very first commands in an interactive Linux machine in your browser
> - Teaching you some essential commands used to interact with the file system
> - Introduce you to how users and groups work on Linux (and what this means for us as penetration testers)

---

## Task 2 - A Bit of Background on Linux

> What year was the first release of a Linux OS?

```
1991
```

---

## Task 3 - Interacting With Your First Linux Machine (In-Browser)

Introduces how to create and access a THM machine in the browser.

---

## Task 4 - Running Your First Few Commands

Introduces basic commands and how we interact with the teminal.

> If we wanted to output the text "**TryHackMe**", what would our command be?

```bash
echo TryHackMe
```

> What is the username of who you're logged in as on your deployed Linux machine?

```bash
~$ whoami
tryhackme
```

---

## Task 5 - Interacting With The Filesystem!

> On the Linux machine that you deploy, how many folders are there?

```
4
```

> Which directory contains a file?

```
folder4
```

> What is the contents of this file?

```
Hello World!
```

> What is the path to that directory?

```
/home/tryhackme/folder4
```

---

## Task 6 - Searching for FIles

> Use ```grep``` on access.log to find the flag.

```
THM{ACCESS}
```

---

## Task 7 - An Introduction to Shell Operators

> If we wanter to run a command in the background, what operatory would we use?

```
&
```

> If I wanted to replace the contents of a file named "passwords" with the word "password123", what would my command be?

```shell
echo password123 > passwords
```

> Now if I wanted to add "tryhackme" to this file named "passwords" but also keep "passwords123", what would my command be?

```shell
echo tryhackme >> passwords
```

---

## Task 8 - Conclusions & Summaries

> To quickly recap, we've covered the following:
> 
> - Understanding why Linux is so commonplace today
> - Interacting with your first-ever Linux machine!
> - Ran some of the most fundamental commands
> - Had
>    an introduction to navigating around the filesystem & how we can 
>   use commands like find and grep to make finding data even more 
>   efficient!
> -  Power up your commands by learning about some of the important shell operators.

---
[[THM-Linux-Fundamentals-2]]