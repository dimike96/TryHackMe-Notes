# THM Linux Fundamentals 2
[TryHackMe | Login](https://tryhackme.com/jr/linuxfundamentalspart2)

> Michael Jack | 06/2022

---

## Task 1 - Intro

> Welcome to the second part of the reworked "Linux Fundamentals" 
> series. We'll be applying our knowledge from the first installment in 
> this series, so I highly recommend you [completing that room](https://tryhackme.com/room/linuxfundamentalspart1) **before** proceeding further.
> 
> In part 2, we'll be ditching the in-browser functionality and help 
> you get started in what is a fundamental skill in being able to login to
>  and control the terminals of remote machines. Not only this, but the 
> room will also have you:
> 
> - Unlocking the potential of your first few commands by introducing you to using flags and arguments
> - Advancing your knowledge of the filesystem to perform some more useful commands such as copying and moving files
> - Introducing you to the access mechanisms in place to keep files and 
>   folders secure and how to identify the things that our current user has 
>   access too
> - Running your first few scripts and executables!

---

## Task 2 - Accessing Your Machine Using SSH (Deploy)

Goes over deploying a machine and an attack machine, and using ssh with them.

```shell
ssh tryhackme@10.10.231.129
```

---

## Task 3 - Introduction to Flags and Switches

> What directional arrow key to go down a man page?

```
down
```

> What flag would we use to display the output in a human readable way?

```shell
ls -h
```

---

## Task 4 - Filesystem Interaction Continued

> How to create a file "newnote"?

```shell
touch newnote
```

> On the deployable machine, what is the file type of "unknown1" in "tryhackme's" home directory?

```shell
ASCII text
```

> How would you move "myfile" to "myfolder"?

```shell
mv myfile myfolder
```

> What are the contents of "myfile"?

```shell
THM{FILESYSTEM}
```

---

## Task 5 - Permissions 101

```shell
total 16K
-rw-r--r-- 1 user2     user2       14 May  5  2021 important
-rw-r--r-- 1 tryhackme tryhackme   16 May  5  2021 myfile
drwxr-xr-x 2 tryhackme tryhackme 4.0K May  4  2021 myfolder
-rw-r--r-- 1 tryhackme tryhackme   17 May  4  2021 unknown1
```

> Who is the owner of "important"?

```
user2
```

> Command to switch to "user2"?

```shell
su user2
```

> Switching to that user, whats the contents of "important"?

```
THM{SU_USER2}
```

---

## Task 6 - Common Directories

> What is the directory we'd expect logs to be in?

```
/var/log
```

> Which directory is similar to how ram works?

```
/tmp
```

> Home directory of the root user?

```
/root
```

---

## Task 7 - Conclusions & Summaries

> Nice work! This room was quite theory-heavy and covered quite a range of the fundamentals in getting you familiar with Linux. To quickly recap, this room taught you:
> 
> - How to connect to a Linux machine remotely using SSH
> - Advancing
>    your use of commands by providing flags, switches and where you can go 
>   to learn about these for each command (man pages)
> - Some more commands that you'll frequently be using to interact with the filesystem and its contents
> - A brief introduction to file permissions & switching users
> - A summary paragraph of the important root directories on a Ubuntu Linux install and how we may be able to use the data stored within these.

---
[[THM Linux Fundamentals 3]]