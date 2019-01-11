---
layout: post
title:  "Linux 101 for Windows devs"
date:   2017-11-27 00:00:00 +0000
categories: [tooling]
---

Todo:
- [ ] Saves images to asset folder
- Spell check in word doc

This article highlights the key points that Windows deveopers or power users need to know when starting out on Linux or Mac.
It is by no means a complete guide - Google is your friend.

I began using and breaking Windows when I was a kid. When I started work as a Data Sciencist at the begining of my carear I was forced to use Linux and Mac and I did so kicking and screaming. I am know a compleete convert but there was a number of things that I found confusing as they were a given in Windows. This article hightlights those things.

# Why Linux?
In a nut shell...
* Productivity
    * High performance applications and user productivity
* Stability
    * No registry - explained below
* Security
    * Multi-user segregated environment - explained below
* Free and open source
    * Most open source software works best or only on Linux
* Market leader for cloud servers
    * [92% of AWS instances are Linux](http://thecloudmarket.com/stats#/totals)

## Linux, Unix, Mac... whats the difference

![Simplified history of Unix-like operating systems. Linux shares similar architecture and concepts (as part of the POSIX standard) but does not share non-free source code with the original Unix or MINIX.](https://i.imgur.com/QZBZlWW.png)

![](https://upload.wikimedia.org/wikipedia/commons/thumb/1/1b/Linux_Distribution_Timeline.svg/232px-Linux_Distribution_Timeline.svg.png){: .align-right}

Unix was developed in the 70s and is the base for Linux, Mac and other systems - which are know as UNIX-like.

Linux itself is not one thing - it can colloquially reference to the Linux kernel, a Linux system, or a Linux distribution. In its most technical sense Linux is just a kernel and ecosystem of components which are compatible with the it. Each component can be added or removed at will as the ecosystem is open source and modular by design. For example in Linux you can separate the graphical interface away from the core of the operating system so that one does not come with another. This is not possible in Windows.

Because each component can be swapped in or out a large ecosystem of Linux distributions exist, each with their own unique combination of programs and capabilities. Have a look at the image on the right which shows the vast landscape of different "distos" and how then relate to each other. The most important distos are:

* Ubuntu - Debian based disto. Good desktop and server support
* Red Hat Enterprise Linux (RHEL) - Commercial (not free) product, has good enterprise support, focus on stability
* CentOS - 100% RHEL compatible, its basically a free version of RHEL. Focused on reliability and stability
* Fedora - RedHat based disto. Focused on quick releases and new features

RHEL used to be the dominate leader, however recently Ubuntu has caught up and [Ubuntu is now the market leader in cloud computing](http://thecloudmarket.com/stats#/totals).

# Linux terminal

![Linux terminal](https://i.imgur.com/aqS9BjH.png)
*Is this it 🤔*

The first thing you will notice is that Linux is primarily a command line (**terminal** or **shell**) based operating system. In contrast to Windows which is based around a graphical user interface (GUI) with windows for each program. This at first seems like a throw back the 70s.

It's very daunting if you have has never used the terminal before, however the terminal is a much more powerful tool for the advanced user (you) and here are some point to consider:

* Terminals require more upfront learning. You need to learn at least a handful of commands as you cant just feel your away around the interface. But once the upfront costs are made you will become much more productive controlling and manipulating the machine.
* Flexible: GUIs generally only have one way of doing a certain thing, while in the terminal there are usually 101 ways of doing the same thing. This flexibility allows you to be more productive, as the terminal includes a library of standard components that can strung together to make complex tasks simple
* Never repeat yourself: you have to repeat yourself a lot in GUIs and can't always automate things. At the terminal everything can be scripted - never do the same task more than twice
* Resources: a GUI requires a large amount of system resources and aren't necessary especially for headless machines

A [full guide to Linux commands](https://www.dedoimedo.com/computers/ultimate-linux-guide-for-windows-users.html#mozTocId796223) is out of scope of this article, but to be productive from the beginning remember these shortcuts that are usually missed by beginners:

* **Ctrl+R**: Reverse search command history
* **Ctrl+A**: Go to the beginning of the line
* **Ctrl+E**: Go to the end of the line.
* **Grep**: Use in conjunction with a pipe to search a long text output of another process. e.g. ps | grep processname

## Drives and mounts

Possibly one of the most confusing things is the lack of drive letters in the file system i.e. there are none. In Windows, each drive is assigned its own letter. In fact, even network shares can be assigned their own drive letters e.g. C:\, D:\, ...

In Linux, the boot drive (i.e. the main drive) is the only drive that is visible at first and starts at the top of the file system which is indicated by the first slash “/” – this is the equivalent to the C:\ drive on my Windows systems. All other drives are mounted or added into this file system.

Typically, a drive will be mounted in the /mnt folder but in it can be done anywhere. e.g. /mnt/d_drive Further info on mounting a drive.

## Paths

Generally, paths are very similar to Windows, here are two examples:

| Linux | /Users/Josh/git/project/example.txt |
| -------- | -------- |
| Windows     | C:\Users\Josh\git\project\example.txt |

1. Paths are case sensitive: you can have multiple files with the different case variations “file”, “File”. This is also important when sharing documents between Windows and Linux and activating autocomplete in bash
1. Paths must use forward slash “/”. Windows can actually use both forward and back slashes but it is custom to use backslashes e.g. “C:\temp”. If your writing programs that need to compatible with both Linux and Windows use forward slashes
1. The current working directory can be referenced with a single dot. Such as as “./file”
1. A users home directory can be referenced using the tilde-prefix e.g. "~/". Note however this is a Bash shortcut and wont work in the wider system. If in doubt use the full path expression.
1. The file extension in Windows dictates how the OS will open the file. This isn't the case in Linux, people just include a file extension for connivance and just indicates the type of file. For text based executables the file type is described using the she-bang, for example python files typically have this included as the first line:
`#!/usr/bin/env python`

## Users and permissions

