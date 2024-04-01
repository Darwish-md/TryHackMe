### Network File System NFS
- In a Network File System (NFS) setup, the server running the NFS service acts as the central point for managing shared files and directories. Clients connect to this server over the network to access the shared resources.
- Using the NFS protocol, you can transfer files between computers running Windows and other non-Windows operating systems, such as Linux, MacOS or UNIX.
- If someone wants to access a file using NFS, an RPC call is placed to NFS daemon on the server. This call takes parameters such as: (file handle, name of the file to be accessed, user ID, group ID).
- NFS runs over port 2049.
- we can use `showmount -e [IP]` to list the NFS shares.
- Now we know a a sharename on the server, we follow these steps to get it on our machine:
  1. we create a directory for example `mkdir /tmp/mount` to mount the share to.
  2. use the command `sudo mount -t nfs <IP>:<sharename> <Directory to mount to: /tmp/mount/> -nolock`.
