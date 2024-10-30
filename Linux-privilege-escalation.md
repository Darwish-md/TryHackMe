# What is privilege escalation?
it's the exploitation of a vulnerability, design flaw, or configuration oversight in an operating system or application to gain unauthorized access to resources that are usually restricted from the users.

# Enumeration
### `hostname`
The hostname command will return the hostname of the target machine. In some cases, it can provide information about the target system’s role within the corporate network (e.g. SQL-PROD-01 for a production SQL server).

### `uname -a`
It will print system information giving us additional detail about the kernel used by the system. This will be useful when searching for any potential kernel vulnerabilities that could lead to privilege escalation.

### /proc/version
The proc filesystem (procfs) provides information about the target system processes. You will find proc on many different Linux flavours.

Looking at `/proc/version`, with `cat`, may give you information on the kernel version and additional data such as whether a compiler (e.g. GCC) is installed.

### /etc/issue
Systems can also be identified by looking at the `/etc/issue` file. This file usually contains some information about the operating system but can easily be customized or changed.

### ps
The ps command is an effective way to see the running processes on a Linux system.

- ps -A: View all running processes
- ps axjf: View process tree
- ps aux to show the processes with their associated users

### env 
The env command will show environmental variables.

The PATH variable may have a compiler or a scripting language (e.g. Python) that could be used to run code on the target system.

### sudo -l
The target system may be configured to allow users to run some (or all) commands with root privileges. The sudo -l command can be used to list all commands your user can run using sudo.

### Id
The id command will provide a general overview of the user’s privilege level and group memberships. 

### /etc/passwd
Reading the /etc/passwd file can be an easy way to discover users on the system.

use command `cat /etc/passwd | cut -d ':' -f 1` to show only name of users. 

Since this shows all users, service and system users, which could be unuseful, we can use `cat /etc/passwd | grep home` to show real users.

### history

### ifconfig

### netstat
The netstat command can be used with several different options to gather information on existing connections.

  - `netstat -a`: shows all listening ports and established connections.
  - `netstat -at` or `netstat -au` can also be used to list TCP or UDP protocols respectively.
  - `netstat -l`: list ports in “listening” mode.
  - `netstat -s`: list network usage statistics by protocol.
  - `netstat -tp`: list connections with the service name and PID information. PID needs to root privilege to get the info for.
  - `netstat -ano`: which could be broken down as follows;
    -a: Display all sockets
    -n: Do not resolve names
    -o: Display timers

### find
Example usage:
- `find / -size 50M`: find files with a 50 MB size
- `find / -type f -perm 0777`: find files with the 777 permissions (files readable, writable, and executable by all users)
- `find /home -user frank`
- `find / -perm -o x -type d 2>/dev/null` : Find world-executable folders
- `find / -perm a=x`: find executable files

Folders and files that can be written to or executed from:
- `find / -writable -type d 2>/dev/null` : Find world-writeable folders
- `find / -perm -222 -type d 2>/dev/null`: Find world-writeable folders
- `find / -perm -o w -type d 2>/dev/null`: Find world-writeable folders

The ***SUID*** bit allows the file to run with the privilege level of the account that owns it, rather than the account which runs it. To find files that have the SUID bit set:
- `find / -perm -u=s -type f 2>/dev/null`

# Automated Enumeration Tools
A few examples: 
- LinPeas: https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS
- LinEnum: https://github.com/rebootuser/LinEnum
- LES (Linux Exploit Suggester): https://github.com/mzet-/linux-exploit-suggester
- Linux Smart Enumeration: https://github.com/diego-treitos/linux-smart-enumeration
- Linux Priv Checker: https://github.com/linted/linuxprivchecker
