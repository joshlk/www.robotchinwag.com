---
layout: post
title:  "Linux 101 for Windows devs"
date:   2017-11-27 00:00:00 +0000
categories: [tooling]
---

This article highlights the key points that Windows developers or power users need to know when starting out on Linux or Mac.
It is by no means a complete guide - Google is your friend.

I began using and breaking Windows when I was a kid. When I started work as a Data Scientist at the beginning of my career I was forced to use Linux and Mac and I did so kicking and screaming. I am now a complete convert but there was a number of things that I found confusing at the start. This article highlights those differences.

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

![Simplified history of Unix-like operating systems. Linux shares similar architecture and concepts (as part of the POSIX standard) but does not share non-free source code with the original Unix or MINIX.](https://i.imgur.com/QZBZlWW.png){:style="max-width:75%; height:auto; display: block; margin-left: auto; margin-right: auto;"}

![Linux Distribution Timeline](https://i.imgur.com/7hQtb9h.png){ :style="max-width:12%; height:auto; float: right; clear: right;"}

 Unix was developed in the 70s and is the base for Linux, Mac and other systems - which are know as UNIX-like.

Linux itself is not one thing - it can colloquially reference to the Linux kernel, a Linux system, or a Linux distribution. In its most technical sense, Linux is just a kernel and ecosystem of components which are compatible with it. Each component can be added or removed at will as the ecosystem is open source and modular by design. For example,  you can separate the graphical interface away from the core of the operating system - one does not necessarily come with another. This is not possible in Windows. 

Because each component can be swapped in or out, a large ecosystem of Linux distributions exists, each with their own unique combination of programs and capabilities. Have a look at the image on the right which shows the vast landscape of different "distros" and how they relate to each other. The most important distros are:

* Ubuntu - Debian based distro. Good desktop and server support
* Red Hat Enterprise Linux (RHEL) - Commercial (not free) product, has good enterprise support, focus on stability
* CentOS - 100% RHEL compatible, it's basically a free version of RHEL. Focused on reliability and stability
* Fedora - RedHat based distro. Focused on quick releases and new features

RHEL used to be the dominant leader, however recently Ubuntu has caught up and [Ubuntu is now the market leader in cloud computing](http://thecloudmarket.com/stats#/totals).

# Linux terminal

![Linux terminal](https://i.imgur.com/aqS9BjH.png){:height="350px" width="auto"}
*Is this it 🤔*

The first thing you will notice is that Linux is primarily a command line based operating system. In contrast to Windows which is based around a graphical user interface (GUI) with windows for each program. This at first seems like a throw back to the 70s.

It's very daunting if you have has never used the terminal before, however, the terminal is a much more powerful tool for the advanced user (you) and here is some point to consider:

* Terminals require more upfront learning. You need to learn at least a handful of commands as you cant just feel you're way around the interface. But once the upfront costs are made you will become much more productive controlling and manipulating the machine.
* Flexible: GUIs generally only have one way of doing a certain thing, while in the terminal there are usually 101 ways of doing the same thing. This flexibility allows you to be more productive, as the terminal includes a library of standard components that can be strung together to make complex tasks simple
* Never repeat yourself: you have to repeat yourself a lot in GUIs and can't always automate things. At the terminal everything can be scripted - never do the same task more than twice
* Resources: a GUI requires a large number of system resources and aren't always necessary - especially for headless machines

A [full guide to Linux commands](https://www.dedoimedo.com/computers/ultimate-linux-guide-for-windows-users.html#mozTocId796223) is out of the scope of this article, but to be productive from the beginning remember these shortcuts that are usually missed by beginners:

* **Ctrl+R**: Reverse search command history
* **Ctrl+A**: Go to the beginning of the line
* **Ctrl+E**: Go to the end of the line.
* **Grep**: Use in conjunction with a pipe to search a long text output of another process. e.g. ps | grep processname

# Drives and mounts

![Linux filesystem strucutre](https://i.imgur.com/4mh1CDT.png){:style="max-width:75%; height:auto; display: block; margin-left: auto; margin-right: auto;"}

Possibly one of the most confusing things is the lack of drive letters in the file system i.e. there are none. In Windows, each drive is assigned its own letter. In fact, even network shares can be assigned their own drive letters e.g. C:\, D:\, ...

In Linux, the boot drive (i.e. the main drive) is the only drive that is visible at first and starts at the top of the file system which is indicated by the first slash “/” – this is the equivalent to the C:\ drive on my Windows systems. All other drives are mounted or added into this file system.

Typically, a drive will be mounted in the /mnt folder but in it can be done anywhere. e.g. /mnt/d_drive Further info on mounting a drive.

# Paths

Generally, paths are very similar to Windows, here are two examples:

| Linux | /Users/Josh/git/project/example.txt |
| Windows     | C:\Users\Josh\git\project\example.txt |

1. Paths are case sensitive: you can have multiple files with the different case variations “file”, “File”. This is also important when sharing documents between Windows and Linux and activating autocomplete in bash
1. Paths must use forward slash “/”. Windows can actually use both forward and back slashes but it is custom to use backslashes e.g. “C:\temp”. If your writing programs that need to compatible with both Linux and Windows use forward slashes
1. The current working directory can be referenced with a single dot. Such as as “./file”
1. A users home directory can be referenced using the tilde-prefix e.g. "~/". Note however this is a Bash shortcut and wont work in the wider system. If in doubt use the full path expression.
1. The file extension in Windows dictates how the OS will open the file. This isn't the case in Linux, people just include a file extension for connivance and just indicates the type of file. For text based executables the file type is described using the she-bang, for example python files typically have this included as the first line:
`#!/usr/bin/env python`

# Users and permissions

Linux is a multi-user OS that is based on the Unix concepts of file ownership and permissions to provide security at the file system level.

In Linux, there are two types of users: *system users* and *regular users*. Traditionally, system users are used to run non-interactive or background processes on a system, while regular users used for logging in and running processes interactively (i.e. through the command line). An easy way to view all of the users on a system is to look at the contents of the `/etc/passwd` file using the command:  `cat /etc/passwd`

In addition to the two user types, there is the *superuser*, or *root* user, that has the ability to override any file ownership and permission restrictions. In practice, this means that the superuser has the rights to access anything on its own server. This user is used to make system-wide changes, and must be kept secure. Some operations, however, do require super-user access and this can be granted temporarily using the sudo command – for example when installing packages see below.

In addition, ever user is a member of a group, which typically by default has the same name as the user. In Linux, each and every file is owned by a single user and a single group, and has its own access permissions.

The most common way to view the permissions of a file is to use `ls` with the long listing option, e.g. `ls -l myfile`. If you want to view the permissions of all of the files in your current directory, run the command without an argument, like this: `ls -l`

Here is an example screenshot of what the output might look like, with labels of each column of output:

![](https://i.imgur.com/MeOSSW7.png)


Aside from the *Mode* column, this listing is fairly easy to understand. To help explain what all the groupings and letters mean, take a look at this closeup of the mode of the first file in the example above:

![](https://i.imgur.com/xGklK01.png)

So for each permission class (user, group and other) its specified if a user can read, write or execute that file. You can change the mode and ownership of a file using the [chmod and chown commands](https://www.pluralsight.com/blog/it-ops/linux-file-permissions).


> Newbies will typically hit a lot of errors because a certain file doesn’t have the right permissions set on it. Check this first if you run into trouble.

# Text files

Linux
![](https://i.imgur.com/LJmcb5c.png)
Windows
![](https://i.imgur.com/DcNSrtz.png)

There is one big difference between Linux and Windows text files: Windows text files use a carriage return followed by a line feed ASCII characters ("\r\n") to dictate the ending of a line, while Unix uses just line feed ("\n").

This can cause a lot of issues when working with text files, especially CSVs, when moving files between Windows and Linux. A lot of programs automatically deal with it while others will not. You can generally convert between the two using a text editor like Notepad++ or Sublime or a command line utility. A typical problem will be all text is rendered on a single line or that extra funny symbols are present in the file.

# Installing programs

Most distrbutions come with a package manger for installing programs. For example, on Unutun to install Postgres you execute:

```
sudo apt-get install postgresql
```

Thats it! No installation wizards, no downloading. You do however require sudo access as discussed above.

__Yer seriously that it 🚀__

# Environment variables

Windows enviroment
![](https://i.imgur.com/9JRRg0f.png)
Linus Enviroment
![](https://i.imgur.com/HNTPmRY.png)

In Linux each process has its own separate set of environment variables. By default, when a process is created, it inherits a duplicate environment of its parent process, except for explicit changes made by the parent when it creates the child. At the OS-API level, these changes must be done between running fork and exec.

This means that an environment variable that is changed in a script or compiled program will only affect that process and possibly child processes. The parent process and any unrelated processes will not be affected.

This is contrast to Windows, whereby changing an enviroment variable changes the global state in the Windows registry and therefore effects all other programs. This is important as the Windows registry acts like a central DB for the OS which grows larger over time when the user installs more programs. This is the main reason why Windows systems slow up over time and need to be whiped clean.

> The abstance of the a central DB or registry is one of the main reasons Linux is a much more stable system compared to Windows.

# Linux in the real world

How many of the top 500 supper computers do you think are powered by Linux?

[All of them!](https://www.linuxfoundation.org/blog/linux-runs-all-of-the-worlds-fastest-supercomputers/)
