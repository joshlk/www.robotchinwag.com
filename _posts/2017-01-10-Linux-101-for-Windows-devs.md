---
layout: post
title:  "Linux 101 for Windows devs"
date:   2017-01-10 00:00:00 +0000
categories: [tooling]
---

This article highlights the key points that Windows developers or power users need to know when starting out on Linux or Mac.
It is by no means a complete guide - Google is your friend.

I began using and breaking Windows when I was a kid. When I started work as a Data Scientist at the beginning of my career I was forced to use Linux and Mac and I did so kicking and screaming. I am now a complete convert but there was a number of things that I found confusing and I wish I know when transitioning between the two systems. This article highlights those differences.

# Why Linux?
In a nutshell...

* __Productivity__
    * High-performance applications and user productivity
* __Stability__
    * No registry - explained below
* __Security__
    * Multi-user segregated environment - explained below
* __Free and open source__
    * Most open source software works best or only on Linux
* __Market leader for cloud servers__
    * [92% of AWS instances are Linux](http://thecloudmarket.com/stats#/totals)

# Linux, Unix, Mac... whats the difference

[![Linux Distribution Timeline](https://i.imgur.com/7hQtb9h.png){:style="max-width:30%; height:auto; float: right; clear: right;"}](https://en.wikipedia.org/wiki/List_of_Linux_distributions#/media/File:Linux_Distribution_Timeline.svg)

[![Simplified history of Unix-like operating systems. Linux shares similar architecture and concepts (as part of the POSIX standard) but does not share non-free source code with the original Unix or MINIX.](https://i.imgur.com/QZBZlWW.png){:style="max-width:70%; height:auto; display: block; "}](https://en.wikipedia.org/wiki/File:Unix_history.svg)

One of the first things that I found confusing when starting was the differences and relationships between UNIX, Linux and MacOS. They all share the same command line interface, file system structure and many other concepts (partially explained in this article) but they are separate systems. As can been from the above timeline UNIX was developed in the 70s and is the base for Linux, Mac and other systems - which are know as UNIX-like.

Linux was developed later using the same concepts but a different code base to UNIX. MacOS separately is based off BSD which again used the same concepts as UNIX. All the systems are roughy POSIX compatible which was a standard developed in the '80s.

Linux itself is not one thing - it can colloquially reference to the Linux kernel, a Linux system, or a Linux distribution. In its most technical sense, Linux is just a kernel and ecosystem of components which are compatible with it. Each component can be added or removed at will as the ecosystem is open source and modular by design. For example, you can separate the graphical interface away from the core of the operating system - one does not necessarily come with another. This is not possible in Windows. 

![Linux filesystem strucutre](https://i.imgur.com/jpzglwb.png){:style="max-width:75%; height:auto; display: block; margin-left: auto; margin-right: auto;"}

Because each component can be swapped in or out, a large ecosystem of Linux distributions exists, each with their own unique combination of programs and capabilities. Have a look at the image on the right which shows the vast landscape of different "distros" and how they relate to each other - as you can see the variation is huge. The most important distros are:

* Ubuntu - Debian based distro. Good desktop and server support. Documentation freely available and open.
* Red Hat Enterprise Linux (RHEL) - Commercial (not free) product, has good enterprise support, focus on stability
* CentOS - 100% RHEL compatible, it's basically a free version of RHEL. Focused on reliability and stability
* Fedora - RedHat based distro. Focused on quick releases and new features

> RHEL used to be the dominant leader, however recently Ubuntu has caught up and [Ubuntu is now the market leader in cloud computing](http://thecloudmarket.com/stats#/totals).

# Linux terminal

![Linux terminal](https://i.imgur.com/aqS9BjH.png){:style="max-width:75%; height:auto; display: block; margin-left: auto; margin-right: auto;"}
*Is this it 🤔*

The first thing you will notice is that Linux is primarily a command line based operating system. In contrast to Windows which is based around a graphical user interface (GUI) with windows for each program. This at first seems like a throwback to the 70s.

It's very daunting if you have has never used the terminal before, however, the terminal is a much more powerful tool for the advanced user (you) 

Terminals require more upfront learning. You need to learn at least a handful of commands as you cant just feel you're way around the interface. But once the upfront costs are made you will become much more productive controlling and manipulating the machine.

The terminal has a number of benefits:

* Flexible: GUIs generally only have one way of doing a certain thing, while in the terminal there are usually 101 ways of doing the same thing. This flexibility allows you to be more productive, as the terminal includes a library of standard components that can be strung together to make complex tasks simple.
* Never repeat yourself: you have to repeat yourself a lot in GUIs as you can't always automate things. At the terminal everything can be scripted - never do the same task more than twice.
* Resources: a GUI requires a large number of system resources and aren't always necessary - especially for headless machines.

A [full guide to Linux commands](https://www.dedoimedo.com/computers/ultimate-linux-guide-for-windows-users.html#mozTocId796223) is out of the scope of this article, but to be productive from the beginning remember these shortcuts that are usually missed by beginners:

* **Ctrl+R**: Reverse search command history
* **Ctrl+A**: Go to the beginning of the line
* **Ctrl+E**: Go to the end of the line.
* **Grep**: Use in conjunction with a pipe to search a long text output of another process. e.g. to search for python processes currently running `ps | grep python`

# Drives and mounts

![Linux filesystem strucutre](https://i.imgur.com/4mh1CDT.png){:style="max-width:75%; height:auto; display: block; margin-left: auto; margin-right: auto;"}

Possibly one of the most confusing things is the lack of drive letters in the file system i.e. there are none. In Windows, each drive is assigned its own letter. In fact, even network shares can be assigned their own drive letters e.g. `C:\`, `D:\`, ...

In Linux, the boot drive (i.e. the main drive) is the only drive that is visible at first and starts at the top of the file system which is indicated by the first slash `/` – this is the equivalent to the `C:\` drive on my Windows systems. All other drives are mounted or added into this file system as subfolders. Typically, a drive will be [mounted](https://www.lifewire.com/uses-of-linux-command-mount-2201110) in the `/mnt` folder but in it can be done anywhere. e.g. `/mnt/d_drive`.

Additionally, other folders such that Windows users will be used to such as `C:\Programs` or `C:\Windows` don't have any direct equivalence in Linux. When you install programs there are multiple places the associated files can be placed which is dependent on the context and usage of the program. Also, a program can typically place files in multiple locations on installation within the filesystem and not just in a single folder such as `C:\Programs\Microsoft_Office`.

# File paths

Generally, paths are very similar to Windows, here are two examples:

* Linux:
    * `/Users/Josh/git/project/example.txt`
* Windows:
    * `C:\Users\Josh\git\project\example.txt`

Things to note:

1. Paths are case sensitive: you can have multiple files with the different case variations “file”, “File”. This is also important when sharing documents between Windows and Linux and activating autocomplete in bash
1. Paths must use forward slash “/”. Windows can actually use both forward and back slashes but it is custom to use backslashes e.g. “C:\temp”. If your writing programs that need to compatible with both Linux and Windows use forward slashes
1. The current working directory can be referenced with a single dot. Such as “./file”
1. A users home directory can be referenced using the tilde-prefix e.g. "~/". Note however this is a Bash shortcut and won't work in the wider system. If in doubt use the full path expression.
1. The file extension in Windows dictates how the command line will execute a file - this isn't the case in Linux. For text-based executables the file type is described using the she-bang, for example, python files typically have this included as the first line of the file e.g. `#!/usr/bin/env python`. This directs the command line to use the process `/usr/bin/env python` to execute the file

# Users and permissions

Linux is a multi-user OS that is based on the Unix concepts of file ownership and permissions to provide security at the file system level.

In Linux, there are two types of users: *system users* and *regular users*. Traditionally, system users run non-interactive or background processes on a system, while regular users are used for logging in and running processes interactively (i.e. through the command line). An easy way to view all of the users on a system is to look at the contents of `/etc/passwd` using the command:  `cat /etc/passwd`

In addition to the two user types, there is the *superuser*, or *root* user, that has the ability to override any file ownership and permission restrictions. In practice, this means that the superuser has the rights to access anything on its own server. This user is used to make system-wide changes and must be kept secure. Some operations, however, do require super-user access and this can be granted temporarily using the `sudo` command – for example when installing packages see below.

In addition, every user is a member of a group, which typically by default has the same name as the user. In Linux, each and every file is owned by a single user and a single group and has its own access permissions.

The most common way to view the permissions of a file is to use `ls` with the long listing option, e.g. `ls -l myfile`. If you want to view the permissions of all of the files in your current directory, run the command without an argument, like this: `ls -l`

Here is an example screenshot of what the output might look like, with labels of each column of output:

[![](https://i.imgur.com/MeOSSW7.png){:style="max-width:75%; height:auto; display: block; margin-left: auto; margin-right: auto;"}](https://www.digitalocean.com/community/tutorials/an-introduction-to-linux-permissions#viewing-ownership-and-permissions)

Aside from the *Mode* column, this listing is fairly easy to understand. To help explain what all the groupings and letters mean, take a look at this closeup of the mode of the first file in the example above:

[![](https://i.imgur.com/xGklK01.png){:style="max-width:60%; height:auto; display: block; margin-left: auto; margin-right: auto;"}](https://www.digitalocean.com/community/tutorials/an-introduction-to-linux-permissions#viewing-ownership-and-permissions)

So for each permission class (user, group and other) its specified if a user can read, write or execute that file. You can change the mode and ownership of a file using the [chmod and chown commands](https://www.pluralsight.com/blog/it-ops/linux-file-permissions).

> Newbies will typically hit a lot of errors because a certain file doesn’t have the right permissions. Check this first if you run into trouble.

# Text files

![](https://i.imgur.com/LJmcb5c.png){:style="max-width:80%; height:auto; "} | ![](https://i.imgur.com/DcNSrtz.png){:style="max-width:80%; height:auto; "}
<center>Linux</center> | <center>Windows</center>

There is one big difference between Linux and Windows text files: Windows text files use a carriage return followed by a line feed ASCII characters ("\r\n") to dictate the ending of a line, while Unix uses just line feed ("\n").

This can cause a lot of issues when working with text files, especially CSVs and when moving files between Windows and Linux. A lot of programs automatically deal with it while others will not. You can generally convert between the two using a text editor like [Notepad++](https://notepad-plus-plus.org/) or [Sublime](https://www.sublimetext.com/) or a command line utility.

> A typical problem will be all text is rendered on a single line or that extra funny symbols are presented in the file.

# Installing programs

Most distributions come with a package manager for installing programs. For example, on Unutun to install Postgres you execute:

```
sudo apt-get install postgresql
```

That's it! No installation wizards, no downloading. You do however require `sudo` access as discussed above.

> Yer seriously that it 🚀

# Environment variables

![](https://i.imgur.com/9JRRg0f.png){:style="max-width:75%; height:auto; "} | ![](https://i.imgur.com/HNTPmRY.png){:style="max-width:75%; height:auto; "}
<center>Windows enviroment</center> | <center>Linux Enviroment</center>

The way Windows and Linux handle environment variables are quite different.

In Linux, each process has its own separate set of environment variables. By default, when a process is created, it inherits a duplicate environment of its parent process, except for explicit changes made by the parent when it creates the child. At the OS-API level, these changes must be done between using `fork` and `exec`.

This means that an environment variable that is changed in a script or compiled program will only affect that process and possibly child processes. The parent process and any unrelated processes will not be affected.

In contrast, Windows, whereby changing an environment variable changes the global state in the Windows registry and therefore affects all other programs. This is important as the Windows registry acts as a central database for the OS and running programs which grows larger over time when the user installs more programs. This is one of the reasons why Windows systems slow up over time.

> The absence of a central database or registry is in part why Linux is more stable when compared to Windows.

# Roundup

Overall Linux and in part Mac, is a more productive, stable and secure environment for the dev or data scientist.

Let me leave you with one last nugget of information...


<details><summary>How many of the top 500 supper computers do you think are powered by Linux?</summary><p>
<div markdown="1">
   **[All of them!](https://www.linuxfoundation.org/blog/linux-runs-all-of-the-worlds-fastest-supercomputers/)**
</div>
</p></details>


---
*Josh Levy-Kramer*

Unless otherwise stated, images are attributed via a link (click on them)

