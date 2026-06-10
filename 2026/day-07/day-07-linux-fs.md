# Day 07 – Linux File System Hierarchy & Scenario-Based Practice

Today's goal is to understand where things live in Linux and practice troubleshooting like a DevOps engineer.
I'll be practicing linux file system hierarchy today.
I have divided the file in 2 section 

* File System Hierarchy 
* Scenario Practice.


## Part 1: Linux File System Hierarchy

	1. / (Root Directory)
Purpose: 
The root directory is the top-level directory in Linux. All files and directories originate from this location.

  **Example Command:**
  ls -l /

  **Observed:**
  home
  etc

  **I would use this when...**
  I need to navigate the Linux filesystem or understand the overall directory structure.




	2. /home (Directory)
   
**Purpose:**
Contains home directories for regular users. Personal files, documents, and user-specific configurations are stored here.

**Command**
ls -l /home


Observed Files/Directories


I would use this when...
I need to access or manage user files and personal settings.

	
	3. /root

**Purpose**
The home directory of the root (administrator) user.

**Command**
ls -la /root

Observed Files/Directories



**I would use this when...**
I am performing administrative tasks as the root user.


	4. /etc
**Purpose**
Stores system-wide configuration files used by Linux services and applications.

**Command**
ls -l /etc

**Observed Files/Directories**

**
I would use this when...**

I need to modify system configurations or troubleshoot service settings.

	5. /var/log
**Purpose**
Contains system and application log files. This directory is extremely important for troubleshooting and monitoring.

**Command**
ls -l /var/log
**Observed Files/Directories**

**I would use this when...**
I need to investigate errors, service failures, or system events.


	6. /tmp
**Purpose**

Stores temporary files created by users and applications.

**Command**
ls -la /tmp
**Observed Files/Directories**

**I would use this when...**
I need a temporary location for testing files or scripts.


## Additional Directories
	7. /bin
Purpose
Contains essential command binaries required for basic system functionality.

Command
ls -l /bin

Observed Files/Directories

aakankshachavan@Aakankshas-MacBook-Air ~ % ls -l /bin
total 9560
-rwxr-xr-x  2 root  wheel   101472  5 Feb 10:43 [
-r-xr-xr-x  1 root  wheel  1310208  5 Feb 10:43 bash

I would use this when...
I need access to basic Linux commands such as ls, cp, and cat.


	8. /usr/bin
Purpose
Contains most user-level command binaries and installed application executables.

Command
ls -l /usr/bin

Observed Files/Directories
aakankshachavan@Aakankshas-MacBook-Air ~ % ls -l /usr/bin
total 171848
-rwxr-xr-x   1 root   wheel    330352  5 Feb 10:43 aa
-rwxr-xr-x  16 root   wheel    119040  5 Feb 10:43 actool

I would use this when...

I need to locate installed command-line tools and applications.


	9. /opt
Purpose

Stores optional and third-party software packages that are not part of the default Linux installation.

Command
ls -l /opt
Observed Files/Directories
aakankshachavan@Aakankshas-MacBook-Air ~ % ls -l /opt
total 0
drwxr-xr-x  28 aakankshachavan  staff   896  4 Jul  2024 anaconda3
drwxr-xr-x  40 aakankshachavan  admin  1280 23 May 16:58 homebrew


I would use this when...

I install or manage third-party applications


## Now Lets do some hands on practice

	# Find the largest log file in /var/log
	du -sh /var/log/* 2>/dev/null | sort -h | tail -5
* du - disk usage, 
* -sh - summary and human readable like KB, MB, GB etc. his shows the size of every file and directory inside /var/log.
* 2>/dev/null - This redirects error messages away.


## Linux has three standard streams:

| Number  | Stream      					  |
| --------|:-----------------------:|
| 0       | stdin (input) 					|
| 1       | stdout (normal output)  |
| 2       | stderr (errors)  			  |


 * What is /dev/null?
> A special device that discards everything sent to it.

* `|` Pipe operator.

> Takes the output of one command and sends it as input to the next command.
>>command1 | command2

* sort -h
> Sorts the output by size.

* tail -5
> Shows the last 5 lines.

> **_NOTE:_**  To quickly identify which logs are consuming the most space, we can use this command.












