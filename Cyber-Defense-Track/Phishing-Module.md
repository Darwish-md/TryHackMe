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

## Pishing prevention:
### SPF (Sender Policy Framework):
Per dmarcian, "Sender Policy Framework (SPF) is used to authenticate the sender of an email. With an SPF record in place, Internet Service Providers can verify that a mail server is authorized to send email for a specific domain. An SPF record is a DNS TXT record containing a list of the IP addresses that are allowed to send email on behalf of your domain."

***Example of SPF record***
> `v=spf1 ip4:127.0.0.1 include:_spf.google.com -all`

### DKIM (DomainKeys Identified Mail):
"DKIM stands for DomainKeys Identified Mail and is used for the authentication of an email that’s being sent. Like SPF, DKIM is an open standard for email authentication that is used for DMARC alignment. A DKIM record exists in the DNS, but it is a bit more complicated than SPF. DKIM’s advantage is that it can survive forwarding, which makes it superior to SPF and a foundation for securing your email."

***Example of DKIM record***
>
```
v=DKIM1; k=rsa; p=MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAxTQIC7vZAHHZ7WVv/5x/qH1RAgMQI+y6Xtsn73rWOgeBQjHKbmIEIlgrebyWWFCXjmzIP0NYJrGehenmPWK5bF/TRDstbM8uVQCUWpoRAHzuhIxPSYW6k/w2+HdCECF2gnGmmw1cT6nHjfCyKGsM0On0HDvxP8I5YQIIlzNigP32n1hVnQP+UuInj0wLIdOBIWkHdnFewzGK2+qjF2wmEjx+vqHDnxdUTay5DfTGaqgA9AKjgXNjLEbKlEWvy0tj7UzQRHd24a5+2x/R4Pc7PF/y6OxAwYBZnEPO0sJwio4uqL9CYZcvaHGCLOIMwQmNTPMKGC9nt3PSjujfHUBX3wIDAQAB
```
- `Authentication-Results` email header shows the status of whether DKIM passed or failed.

### DMARM (Domain-based Message Authentication Reporting, & Conformance):
"DMARC, (Domain-based  Message Authentication Reporting, & Conformance) an open source standard, uses a concept called alignment to tie the result of two other open source standards, SPF (a published list of servers that are authorized to send email on behalf of a domain) and DKIM (a tamper-evident domain seal associated with a piece of email), to the content of an email. If not already deployed, putting a DMARC record into place for your domain will give you feedback that will allow you to troubleshoot your SPF and DKIM configurations if needed."

***Example of DKIM record***
`v=DMARC1; p=quarantine; rua=mailto:postmaster@website.com`

### S/MIME 
Per Microsoft, "S/MIME (Secure/Multipurpose internet Mail Extensions) is a widely accepted protocol for sending digitally signed and encrypted messages.". It guarantees data integrity and nonrepudiation.
- Nonrepudiation: The uniqueness of a signature prevents the owner of the signature from disowning the signature. It prevents the sender of the data from claiming, at a later date, that the data was never sent.
## Notes:
- The syntax for email messages is known as the Internet Message Format (IMF).
- A BEC (Business Email Compromise) is when an adversary gains control of an internal employee's account and then uses the compromised email account to convince other internal employees to perform unauthorized or fraudulent actions.
- A single `tracking pixel` is embedded in the email, usually (but not always) hidden within an image or a link. When the email is opened, code within the pixel sends the info back to the company’s server. 
- A typosquatting attack, also known as a URL hijacking, a sting site, or a fake URL, is a type of social engineering where threat actors impersonate legitimate domains for malicious purposes.
- BCC (Blind Carbon Copy):  When you place email addresses in the BCC field of a message, those addresses are invisible to the recipients of the email. 
- Ray Tomlinson invented the concept of emails and made @ symbol famous.
- Malware sandboxes are online tools and services where malicious files can be uploaded and analyzed to better understand what the malware was programmed to do. 
