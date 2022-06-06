# THM Linux Fundamentals 3
[TryHackMe | Linux Fundamentals Part 3](https://tryhackme.com/room/linuxfundamentalspart3)

> Michael Jack | 06/2022

---

## Task 1 - Intro

> Welcome to part three (and the finale) of the Linux Fundamentals module. So far, throughout the series, you have got 
> hands-on with some fundamental concepts and used some important 
> commands. This room is going to showcase some useful utilities and 
> applications that you are likely to use day-to-day. You're also going to
>  advance your Linux-fu skills by learning about automation, package 
> management, and service/application logging.

---

## Task 2 - Deploy Your Linux Machine

---

## Task 3 - Terminal Text Editors

Introduction to Nano, and Vim as an alternative to explore later.

> Create a file using Nano

```shell
nano NewFile.txt
```

> Edit "task3" located in "tryhackme"'s home directory. Whats the flag?

```
THM{TEXT_EDITORS}
```

---

## Task 4 - General/Useful Utilities

- Downloading files
  - ```wget https://domain.com/path/to/file.extension```

- Transfering files from your host - SCP (SSH)

  - Secure copy (SCP) allows transfering files between to computers using the SSH protocol to provide authentication and encryption.

  - ```scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt```

  - ^ copies important.txt from the local machine to transferred.tx in the /home/ubuntu directory of the remote machine

  - ```scp ubuntu@192.168.1.30:/home/ubuntu/documents.txt notes.txt```

  - ^ Tranfers /home/ubuntu/documents.txt from a remote machine to a notes.txt on our local machine.

- Serving files from your host - WEB

  - > Ubuntu machines come pre-packaged with python3. Python helpfully 

    > provides a lightweight and easy-to-use module called "HTTPServer". This 
    > module turns your computer into a quick and easy web server that you can
    >  use to serve your own files, where they can then be downloaded by 
    > another computing using commands such as `curl` and `wget`.

  - All we need to start the module is `python3 -m  http.server`
    
    - Will start from the working directory by default. See man page for HTTPServer.
    
    - We need the full path to any file we want to download using ```wget``` .
  
  > Start a web server in the tryhackme home directory and wget .flag.txt. What is the flag?
  
  ```
  THM{WGET_WEBSERVER}
  ```
  
  ---
  
  ## Task 5 - Processes 101

### Viewing Processes

We can view processes by running ```ps```.

By default ```ps``` doesn't show processes run by other users, or that don't run from a session (system processes). To see those we can add aux tot he command. So ```ps aux```.

> Another very useful command is the ```top``` command top gives you real-time 
> statistics about the processes running on your system instead of a 
> one-time view. These statistics will refresh every 10 seconds, but will 
> also refresh when you use the arrow keys to browse the various rows.

### Managing Processes

We can send signals to processes. We can send different signals to terminate them depending on how "cleanly" we want it done.

- SIGTERM - Kill the process, but allow it to do some cleanup tasks beforehand

- SIGKILL - Kill the process - doesn't do any cleanup after the fact

- SIGSTOP - Stop/suspend a process
  
  ### How do Processes Start?

> Let's start off by talking about namespaces. The Operating System (OS) uses namespaces to ultimately split up the resources available on the computer to (such as CPU, RAM and priority) processes. Think of it as splitting your computer up into slices -- similar to a cake. Processes within that slice will have access to a certain amount of computing power, however, it will be a small portion of what is actually available to every process overall. 
> 
> Namespaces are great for security as it is a way of isolating processes from another -- only those that are in the same namespace will be able to see each other.
> 
> We previously talked about how PID works, and this is where it comes into play. The process with an ID of 0 is a process that is started when the system boots. This process is the system's init on Ubuntu, such as **systemd**, which is used to provide a way of managing a user's processes and sits in between the operating system and the user. 
> 
> For example, once a system boots and it initialises, **systemd** is one of the first processes that are started. Any program or piece of software that we want to start will start as what's known as a child process of **systemd**. 
> This means that it is controlled by **systemd**, but will run as its own process (although sharing the resources from **systemd**) to make it easier for us to identify and the likes.

### Getting Processes/Services to Start on Boot

The ```systemctl``` command allows us to interact with the systemd process/daemon. Used like ```systemctl [option] [service]```.

The options are:

- Start

- Stop

- Enable

- Disable

### An Introduction to Backgrounding and Foregrounding Tasks in Linux

Processes either run in the foreground or the background. We can use the ```&``` operator at the end of a command to run it in the background.

We can do the same with scripts, and also rather than relying solely on the ```&``` operator we can use ```ctrl + z``` on the keyboard 

If we want to go the otherway and foreground a process we can run ```ps aux``` to find it and use the ```fg``` command to bring it to the foreground.

> If we lauch a process after the process with pip 300 what would the new pid be?

```
301
```

> If we wanted to cleanly kill a process what signal do we send?

```
SIGTERM
```

The default signal of the ```kill``` command is SIGTERM.

> Locate the flag shown in the processes running on the machine.

```
THM{PROCESSES}
```

> What command would you use to stop the service "myservice"?

```shell
systemctl stop myservice
```

> What command would make that service start at boot?

```shell
systemctl enable myservice
```

> What command foregrounds a backgrounded process?

```shell
fg
```

---

## Task 6 - Maintaining Your System: Automation

A crontab is simply a special file with formatting that is recognised by the `cron` process to execute each line step-by-step. Crontabs require 6 specific values:

- MIN - minute to exec

- HOUR - hour to exec

- DOM - day of the month to exec

- MON - moth of year to exec

- DOW - day of week to exec

- CMD - command to exec

Let's use the example of backing up files. You may wish to backup 
"cmnatic"'s  "Documents" every 12 hours. We would use the following 
formatting: 

`0 *12 * * * cp -R /home/cmnatic/Documents /var/backups/`

An interesting feature of crontabs is that these also support the wildcard or asterisk (`*`).
 If we do not wish to provide a value for that specific field, i.e. we 
don't care what month, day, or year it is executed -- only that it is 
executed every 12 hours, we simply just place an asterisk.

This can be confusing to begin with, which is why there are some great resources such as the online "[Crontab Generator](https://crontab-generator.org/)" that allows you to use a friendly application to generate your formatting for you! As well as the site "[Cron Guru](https://crontab.guru/)"!

Crontabs can be edited by using `crontab -e`, where you can select an editor (such as Nano) to edit your crontab.

> When will the crontab on the machine run?

```
@reboot
```

---

## Task 7 - Maintaining Your System: Package Management

Introduction to package management with apt.

Introduces repos, adding developers GPG keys, creating .list files in /etc/apt/sources.list.d, and running ```apt update``` and ```apt install package-name```.

---

## Task 8 - Maintaining Your System: Logs

> We briefly touched upon log files and where they can be found in Linux Fundamentals Part 1. However, let's quickly recap. Located in the 
> /var/log directory, these files and folders contain logging information 
> for applications and services running on your system. The Operating 
> System  (OS) has become pretty good at automatically managing these logs in a process that is known as "rotating".

logs for services such as a web server contain information about 
every single request - allowing developers or administrators to diagnose performance issues or investigate an intruder's activity. For example, the two types of log files below that are of interest:

- access log
- error log

> What is the IP address of the user who visited the apache site?

```
10.9.232.111
```

> What file did they access?

```
catsanddogs.jpg
```

---

## Task 9 - Conclusions & Summaries

To recap, this room introduced you to the following topics:

- Using terminal text editors
- General utilities such as downloading and serving contents using a python webserver
- A look into processes
- Maintaining & automating your system by the use of crontabs, package management, and reviewing logs

Continue your learning in some other TryHackMe rooms that are dedicated to Linux tools or utilities:

- The find command - [TryHackMe | The find command](https://tryhackme.com/room/thefindcommand)
- Bash Scripting - [TryHackMe | Bash Scripting](https://tryhackme.com/room/bashscripting)
- Regular Expressions - [TryHackMe | Regular expressions](https://tryhackme.com/room/catregex)


