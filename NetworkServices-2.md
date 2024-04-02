### Network File System NFS
- In a Network File System (NFS) setup, the server running the NFS service acts as the central point for managing shared files and directories. Clients connect to this server over the network to access the shared resources.
- Using the NFS protocol, you can transfer files between computers running Windows and other non-Windows operating systems, such as Linux, MacOS or UNIX.
- If someone wants to access a file using NFS, an RPC call is placed to NFS daemon on the server. This call takes parameters such as: (file handle, name of the file to be accessed, user ID, group ID).
- NFS runs over port 2049.
- we can use `showmount -e [IP]` to list the NFS shares.
- Now we know a a sharename on the server, we follow these steps to get it on our machine:
  1. we create a directory for example `mkdir /tmp/mount` to mount the share to.
  2. use the command `sudo mount -t nfs <IP>:<sharename> <Directory to mount to: /tmp/mount/> -nolock`.

### Simple Mail Transfer Protocol SMTP
It is utilised to handle the sending of emails.

Here is the process of sending an email:
  1. The mail user agent, which is either your email client or an external program. connects to the SMTP server of your domain, e.g. smtp.google.com. This initiates the SMTP handshake. This connection works over the SMTP port- which is usually 25. Once these connections have been made and validated, the SMTP session starts.
  2. The process of sending mail can now begin. The client first submits the sender, and recipient's email address- the body of the email and any attachments, to the server.
  3. The SMTP server then checks whether the domain name of the recipient and the sender is the same.
  4. The SMTP server of the sender will make a connection to the recipient's SMTP server before relaying the email. If the recipient's server can't be accessed, or is not available- the Email gets put into an SMTP queue.
  5. Then, the recipient's SMTP server will verify the incoming email. It does this by checking if the domain and user name have been recognised. The server will then forward the email to the POP or IMAP server, as shown in the diagram above.
  6. The E-Mail will then show up in the recipient's inbox.
