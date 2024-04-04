- To add credentials for an RDP, we can use this cmnd `cmdkey /generic:TERMSRV/<targetname> /user: "<username>" /pass: "<password>"`, where targetname is the rdp file name that we can find if we open it in notepad.
- ***Seclists*** is an amazing collection of wordlists. it can be installed with `sudo apt install seclists` if using Kali or Parrot. Alternatively, we can download the repository from the repository. We also have `rockyou.txt` under directory `usr/share/wordlists` for password cracking. 
- ***Hydra*** is a very fast online password cracking tool, which can perform rapid dictionary attacks against more than 50 Protocols, including Telnet, RDP, SSH, FTP, HTTP, HTTPS, SMB, several databases and much more. Command syntax is as following: `hydra -t <Number of parallel connections per target> -l <username> -P <wordlist.txt file path> -vV <Target_IP> <service like ftp, smb, etc>`.
  
### During Windows Investigation room:
1. To find the system information, from cmd: `systeminfo`.
2. To find all user accounts on system, we can use `net user`. To find information about a specific user: `net user <username>`.
3. To access the user manager, from Run we type `lusrmgr.msc`.
4. For persistence of tasks/commands/connections on system start, we check the autoruns/autostart programs in the registry, or use `Get-Item` like here: `Get-Item "Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run"`.
5. For persistence of scheduled tasks, we check in `C:\Windows\System32\Tasks` or in the task scheduler, or we use `Get-ScheduledTask`.
6. "Inetpub" is a directory commonly found on Windows servers. It stands for "Internet Publishing" and serves as the default root directory for IIS websites and contains the web content, configuration files, and other resources related to hosting websites. If any files are uploaded via server's website, it should be there.
7. The hosts file located at `C:\Windows\System32\drivers\etc\hosts` is a plain text file used by OSs to map hostnames to IP addresses before querying DNS servers. It's commonly used to override DNS mappings or to block access to specific websites by redirecting their domain names to localhost or other IP addresses. If suspecting DNS poisoning, this needs to be checked and usually there we will find the C2 IP, targeted domain, etc..
8. We should be always checking for new firewall rules, since there connections can be allowed to C2 servers, or specific ports for inbound connections, etc..

### During Attacktive Directory
- In the beginning, we need to know the open ports, AD domain name which can be obtained with nmap basic flags: `nmap -sV -sC -oN nmap.out 10.10.151.9`.
- We use `Enum4Linux` to enumerate running services on the server as well as getting info like NetBIOS domain.
- If Kerberos was found to be runnning, then we can use `kerbrute` tool to enumerate the valid usernames against a list of usernames.
- After the enumeration of user accounts is finished, we can attempt to abuse a feature within Kerberos with an attack method called ***ASREPRoasting***. ASReproasting occurs when a user account has the privilege "Does not require Pre-Authentication" set. Impacket has a tool called "GetNPUsers.py" which can be used for that. It returns the vunerable users and their hash.
- once we have a valid user password hash, we can crack this password using hashcat, `hashcat -m <hash_mode> <hash_file> <wordlist_file>`. hash mode can be obtained from hashcat examples wikipage.
- Once we have an valid account credentials, we then use smbclient to list shares `smbclient -L //10.10.151.9 -U svc-admin` and we provide the account's password. we can then check a specific share like `smbclient //10.10.151.9/sharename -U svc-admin`
- `secretsdump.py` is a tool used for extracting password hashes and other credential information from Windows systems, particularly from the NTDS.DIT database in Active Directory environments (like mimikatz). It can be used as in the following: `secretsdump.py -dc-ip 10.10.151.9 <domain_name>/<username>:<password>@10.10.151.9`. As far as I understand, this username account has unique permissions like a backup account for the Domain controller, so it has all NTLM hashes of AD synced.
- If we get to know the NTLM hash of a user, we can use `evil-winrm -i 10.10.151.9 -u <username> -H <Hash>` to establish a connection (Pass the Hash).
