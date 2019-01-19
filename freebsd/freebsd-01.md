# Freebsd
---
[TOC]
---
## 1.基础
1. 开机后查看开机信息
```bash
dmesg
```
+++
	dmesg - display the system message bufer
	dmesg [-ac][-M core [-N system]]
	The dmesg utility displays the contents of the system message buffer.  If the -M option is not specified, the buffer is read from the currently running kernel via the sysctl(3) interface.  Otherwise, the buffer is read from the specified core file, using the name list from the specified kernel image (or from the default image)
	
	-a	Show all data in the message buffer. This includes any syslog records and /dev/console output.
	-c	Clear the kernel buffer after printing.
	-M	Extract values associates with the name list from the specified core.
	-N	If -M is also specified, extract the name list from the specified system instead of the default, which is the kernel image the system has booted from.
	/var/run/dmesg.boot	usually a snapshot of the buffer contents taken soon after file systems are mounted at startup time

+++

2. 关闭Freebsd
```bash
shutdown -p now
```
+++
	Shutdown,powoff - close down the system at a given time
	shutdown [-][-h | -p | -r | -k] [-o [-n]] time [warning-message ...]
	The shutdown utility provides an automated shutdown procedure for super users to nicely notify users when the system is shutting down.
	
	-h The system is halted at the specified time.
	-p The system is halted and the power is turned off at the specified time.
	-r The system is rebooted at the specified time.
	-k Kick everybody off.The -k option does not actually halt the system, but leaves the system multi-user with logins disabled (for all but super-user).
	-o If one of the -h, -p or -r options are specified, shutdown will execute halt(8) or reboot(8) instead of sending a signal to init(8).
	-n If the -o option is specified, prevent the file system cache from being flushed by passing -n to halt(8) or reboot(8).  This option should probably not be used.
	Time -> Time is the time at which shutdown will bring the system down and may be the case-insensitive word now (indicating an immediate shutdown) or a future time in one of two formats: +number, or yymmddhhmm, where the year, month, and day may be defaulted to the current system values.  The first form brings the system down in number minutes and the second at the absolute time specified. +number may be specified in units other than minutes by appending the corresponding suffix: "s", "sec", "m", "min". "h", "hour".
	warning-message -> Any other arguments comprise the warning message that is broadcast to users currently logged into the system.
	- If `-' is supplied as an option, the warning message is read from the standard input.
	At intervals, becoming more frequent as apocalypse approaches and starting at ten hours before shutdown, warning messages are displayed on the terminals of all users logged in.  Five minutes before shutdown, or immediately if shutdown is in less than 5 minutes, logins are disabled by creating /var/run/nologin and copying the warning message there.  If this file exists when a user attempts to log in, login(1) prints its contents and exits.  The file is removed just before shutdown exits.
	At shutdown time a message is written to the system log, containing the time of shutdown, the person who initiated the shutdown and the reason. The corresponding signal is then sent to init(8) to respectively halt, reboot or bring the system down to single-user state (depending on the above options).  The time of the shutdown and the warning message are placed in /var/run/nologin and should be used to inform the users about when the system will be back up and why it is going down (or anything else).
	A scheduled shutdown can be canceled by killing the shutdown process (a SIGTERM should suffice).  The /var/run/nologin file that shutdown created will be removed automatically.
	When run without options, the shutdown utility will place the system into single user mode at the time specified.
	Calling "poweroff" is equivalent to running
	```
	shutdown -p now
	```

+++
