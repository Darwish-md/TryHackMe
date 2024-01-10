## SMB
- SMB, Server Message Block Protocol, is a client-server communication protocol used for sharing access to files, printers, serial ports and other resources on a network.
- Servers make file systems and other resources (printers, named pipes, APIs) available to clients on the network.
- Once clients have established a connection, clients can then send commands (SMBs) to the server that allow them to access shares, open files, read and write files, and generally do all the sort of things that you want to do with a file system. However, in the case of SMB, these things are done over the network.
- Clients connect to servers using TCP/IP (actually NetBIOS over TCP/IP as specified in RFC1001 and RFC1002), NetBEUI or IPX/SPX.

### Enumeration
 - It is the process of gathering information on a target in order to find potential attack vectors and aid in exploitation.
 - It can be used to gather usernames, passwords, network information, hostnames, application data, services, or any other information that may be valuable to an attacker.

- SMB runs on ports 139/tcp netbios-ssn and 445/tcp microsoft-ds

  
