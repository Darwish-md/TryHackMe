The Sysinternals tools is a compilation of over 70+ Windows-based tools.

### Add to system variables to run from cmd:
- The System Properties can be launched via the command line by running `sysdm.cpl`. Click on the Advanced tab.
- Add the path to the `System variables`.

### Run sysinternals:
- To run sysinternals, we can downaload and install the suite\specific tool, or we can run it from live.sysinternals.com.
#### Prerequistes to run the live version:
1. Network Discovery needs to be enabled:
   - Use command `control.exe /name Microsoft.NetworkAndSharingCenter`.
   - Click on Change advanced sharing settings and select Turn on network discovery for your current network profile.
2. Install WebDAV Redirector: `Install-WindowsFeature WebDAV-Redirector –Restart` and verify using `Get-WindowsFeature WebDAV-Redirector | Format-Table –Autosize`
3. The WebDAV client must be installed and running on the machine. The WebDAV protocol is what allows a local machine to access a remote machine running a WebDAV share and perform actions in it.
   - On a Windows 10 client, the WebDAV client is installed but the client is most likely not running. to verify the status: `get-service webclient` and to start it `start-service webclient`.
4. run a tool like `\\live.sysinternals.com\tools\procmon`.

## Let's go through some example tools:
### File and Disk utilities:
#### sigcheck
This is a tool used to check for file signatures. 
- An example would be `sigcheck -u -e C:\Windows\System32` which checks for any file which has unknown signature according to VT. if the result shows any file, that would mean there is sth wrong.
- It can also be used to show info about a specific file `sigcheck file_path`.
#### streams
- Streams: Streams refer to the main data content of a file. Every file in NTFS has at least one stream, which contains the primary data associated with the file, such as text, images, or executable code.
- Alternate Data Streams (ADS): ADS is a feature of NTFS that allows additional data streams to be associated with a file. These additional streams can contain metadata, additional content, or even executable code. ADS allows for the storage of multiple pieces of information within a single file, without altering the original file's content.
- streams utility is used to display and manipulate alternate data streams (ADS) associated with files on Windows NTFS volumes.
#### SDelete
- SDelete is a command line utility that takes a number of options. In any given use, it allows you to delete one or more files and/or directories, or to cleanse the free space on a logical disk.
- SDelete has been used by adversaries and is associated with MITRE techniques T1485 (Data Destruction) and T1070.004 (Indicator Removal on Host: File Deletion). It's MITRE ID S0195.

### Networking utilities:
#### TCPView
TCPView is a Windows program that will show you detailed listings of all TCP and UDP endpoints on your system, including the local and remote addresses and state of TCP connections. 
> There is a pre-installed service called `resmon` which has the same purpose as TCPView.

### Process utilities:
#### Autoruns
It is used for monitoring and managing the various programs, processes, drivers, and services that automatically start and run when a Windows system boots up or a user logs in.
> This is a good tool to search for any malicious entries created in the local machine to establish Persistence.
#### ProcDump
It monitors a process and writes a dump file whenever the process exceeds the specified criteria or has an exception (Monitoring for CPU spikes).
#### ProcExp
The Process Explorer display consists of two sub-windows. The top window always shows a list of the currently active processes, including the names of their owning accounts, whereas the information displayed in the bottom window depends on the mode that Process Explorer is in: if it is in handle mode you'll see the handles that the process selected in the top window has opened; if Process Explorer is in DLL mode you'll see the DLLs and memory-mapped files that the process has loaded."
#### procMon
"Process Monitor is an advanced monitoring tool for Windows that shows real-time file system, Registry and process/thread activity. It combines the features of two legacy Sysinternals utilities, Filemon and Regmon, and adds an extensive list of enhancements including rich and non-destructive filtering, comprehensive event properties such as session IDs and user names, reliable process information, full thread stacks with integrated symbol support for each operation, simultaneous logging to a file, and much more. Its uniquely powerful features will make Process Monitor a core utility in your system troubleshooting and malware hunting toolkit."
#### PsExec
PsExec is a light-weight telnet-replacement that lets you execute processes on other systems.

### Security utilities:
#### Sysmon
System Monitor (Sysmon) is a Windows system service and device driver that, once installed on a system, remains resident across system reboots to monitor and log system activity to the Windows event log.

### System Information:
#### WinObj
"WinObj is a 32-bit Windows NT program that uses the native Windows NT API (provided by NTDLL.DLL) to access and display information on the NT Object Manager's name space."
> NT Object Namespace is a hierarchical database-like structure used by the Windows kernel to manage various system resources and objects. It provides a unified and organized way to represent and access system resources, such as files, devices, processes, threads, registry keys, synchronization objects, and more.

### Miscellaneous
#### BgInfo
"It automatically displays relevant information about a Windows computer on the desktop's background, such as the computer name, IP address, service pack version, and more."
#### RegJump
"This little command-line applet takes a registry path and makes Regedit open to that path. It accepts root keys in standard (e.g. HKEY_LOCAL_MACHINE) and abbreviated form (e.g. HKLM)." 
- There are multiple ways to query the Windows Registry without using the Registry Editor, such as via the command line (`reg query`) and PowerShell (`Get-Item`/`Get-ItemProperty`).
- Using Regjump will open the Registry Editor and automatically open the editor directly at the path, so one doesn't need to navigate it manually.
#### Strings
It is used for extracting readable text strings from binary files. It is commonly used in cybersecurity and software development contexts to analyze executable files, libraries, firmware, and other binary data for human-readable text.
- The following example shows how to look for all strings containing the chars pdb in the exec ZoomIt.exe: `strings C:\Tools\sysint\ZoomIt.exe | findstr /i pdb`.
