-  Ray Tomlinson invented the concept of emails and made @ symbol famous.

## There are 3 protocls associated with the process of sending emails:
1. SMTP (Simple Mail Transfer Protocol) - It is utilized to handle the sending of emails. It is the de facto standard for outgoing email transmissions across the Internet.
 AND  
2. POP3 (Post Office Protocol) OR
4. IMAP (Internet Message Access Protocol) - responsible transferring email between a client and a mail server.

![image](https://github.com/Darwish-md/TryHackMe/assets/72353586/3170bbf0-d393-4b7e-9eb3-e4898f96eaa2)

## Differences between IMAP & POP3:
### POP3:
- it downloads all mail from the server from the Inbox and stores it on your computer. This way, emails are available when you're not connected to the Internet. You also have the option (in your mail client) to keep email on the server.
### IMAP:
- IMAP syncs your mail client program with the server. Since emails stay on the server, you can see all your emails from any mail client program or device.

## Ports:
### Incoming:
- IMAP | Port 993 (Secure Transport   — SSL function enabled) RECOMMENDED.
- POP3 | Port 995 (Secure Transport   — SSL function enabled)
- IMAP | Port 143 (Insecure Transport — No SSL function enabled)
- POP3 | Port 110 (Insecure Transport — No SSL function enabled)
### Outgoing:
- SMTP | Port 465 (Secure Transport — SSL function enabled)
- SMTP | Port 587 (Insecure Transport, but can be upgraded to a secure connection using STARTTLS).
- SMTP | Port 25 (Outdated and not recommended. username/password authentication MUST be enabled if using this port.)
