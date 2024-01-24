## SMB
- SMB, Server Message Block Protocol, is a client-server communication protocol used for sharing access to files, printers, serial ports and other resources on a network.
- Servers make file systems and other resources (printers, named pipes, APIs) available to clients on the network.
- Once clients have established a connection, clients can then send commands (SMBs) to the server that allow them to access shares, open files, read and write files, and generally do all the sort of things that you want to do with a file system. However, in the case of SMB, these things are done over the network.
- Clients connect to servers using TCP/IP (actually NetBIOS over TCP/IP as specified in RFC1001 and RFC1002), NetBEUI or IPX/SPX.
- SMB runs on ports 139/tcp netbios-ssn and 445/tcp microsoft-ds
  
### Enumeration
- It is the process of gathering information on a target in order to find potential attack vectors and aid in exploitation.
- It can be used to gather usernames, passwords, network information, hostnames, application data, services, or any other information that may be valuable to an attacker.
- `enum4linux [options] ip` can be used to enumerate SMB shares on both Windows and Linux systems.
- After getting to know the share names on a server, We can remotely access the SMB share using the syntax: `smbclient //[IP]/[SHARE]` Followed by the tags: -U [name] : to specify the user -p [port] : to specify the port

### NMAP
- To look for open ports in the most common 1000 ports: `nmap ip`
- for all ports: `nmap -p- ip`, for range of ports `nmap -p x-y ip`
- `-sV`: Enables service version detection. It attempts to determine the version of the running services on the target.
- `-A`: Aggressive scan. It includes additional features like OS detection, script scanning, and traceroute.

## Telnet
- Telnet is an application protocol which allows you, with the use of a telnet client, to connect to and execute commands on a remote machine that's hosting a telnet server.
- You can connect to a telnet server with the following syntax: `telnet [ip] [port]`
- Telnet has been replaced by SSH in most implementations in some applications due to the vulnerabilities discovered and that it sends messages in clear text.
> A "shell" can simply be described as a piece of code or program which can be used to gain code or command execution on a device. A reverse shell is a type of shell in which the target machine communicates back to the attacking machine. The attacking machine has a listening port, on which it receives the connection, resulting in code or command execution being achieved.
-

## FTP
- File Transfer Protocol (FTP) is a protocol used to allow remote transfer of files over a network. It uses a client-server model to do this.
- FTP session operates using two channels: [1] a command (sometimes called the control) channel [2] a data channel.
- The FTP server may support either Active or Passive connections, or both.
  - In an Active FTP connection, the client opens a port and listens. The server is required to actively connect to it. 
  - In a Passive FTP connection, the server opens a port and listens (passively) and the client connects to it. 
  
