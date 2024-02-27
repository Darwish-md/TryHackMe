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

## Phishing:
Different types of malicious emails can be classified as one of the following:
- Spam - unsolicited junk emails sent out in bulk to a large number of recipients. The more malicious variant of Spam is known as MalSpam.
- Phishing -  emails sent to a target(s) purporting to be from a trusted entity to lure individuals into providing sensitive information. 
- Spear phishing - takes phishing a step further by targeting a specific individual(s) or organization seeking sensitive information.  
- Whaling - is similar to spear phishing, but it's targeted specifically to C-Level high-position individuals (CEO, CFO, etc.), and the objective is the same. 
- Smishing - takes phishing to mobile devices by targeting mobile users with specially crafted text messages. 
- Vishing - is similar to smishing, but instead of using text messages for the social engineering attack, the attacks are based on voice calls.
  
## Notes:
- The syntax for email messages is known as the Internet Message Format (IMF).
- A BEC (Business Email Compromise) is when an adversary gains control of an internal employee's account and then uses the compromised email account to convince other internal employees to perform unauthorized or fraudulent actions.
- A single `tracking pixel` is embedded in the email, usually (but not always) hidden within an image or a link. When the email is opened, code within the pixel sends the info back to the company’s server. 
- A typosquatting attack, also known as a URL hijacking, a sting site, or a fake URL, is a type of social engineering where threat actors impersonate legitimate domains for malicious purposes.
- BCC (Blind Carbon Copy):  When you place email addresses in the BCC field of a message, those addresses are invisible to the recipients of the email. 
- Ray Tomlinson invented the concept of emails and made @ symbol famous.
- Malware sandboxes are online tools and services where malicious files can be uploaded and analyzed to better understand what the malware was programmed to do. 
