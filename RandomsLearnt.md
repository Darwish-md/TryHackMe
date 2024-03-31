### During Windows Investigation room:
1. To find the system information, from cmd: `systeminfo`.
2. To find all user accounts on system, we can use `net user`. To find information about a specific user: `net user <username>`.
3. To access the user manager, from Run we type `lusrmgr.msc`.
4. For persistence of tasks/commands/connections on system start, we check the autoruns/autostart programs in the registry, or use `Get-Item` like here: `Get-Item "Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run"`.
5. For persistence of scheduled tasks, we check in `C:\Windows\System32\Tasks` or in the task scheduler, or we use `Get-ScheduledTask`.
6. "Inetpub" is a directory commonly found on Windows servers. It stands for "Internet Publishing" and serves as the default root directory for IIS websites and contains the web content, configuration files, and other resources related to hosting websites. If any files are uploaded via server's website, it should be there.
7. The hosts file located at `C:\Windows\System32\drivers\etc\hosts` is a plain text file used by OSs to map hostnames to IP addresses before querying DNS servers. It's commonly used to override DNS mappings or to block access to specific websites by redirecting their domain names to localhost or other IP addresses. If suspecting DNS poisoning, this needs to be checked and usually there we will find the C2 IP, targeted domain, etc..
8. We should be always checking for new firewall rules, since there connections can be allowed to C2 servers, or specific ports for inbound connections, etc..
