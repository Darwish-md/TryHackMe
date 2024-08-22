### Kerberos
Kerberos is a computer network authentication protocol that operates based on tickets, allowing nodes to securely prove their identity to one another over a non-secure network. It primarily aims at a client-server model and provides mutual authentication, where the user and the server verify each other's identity. The Kerberos protocol messages are protected against eavesdropping and replay attacks, and it builds on symmetric-key cryptography, requiring a trusted third party.

![image](https://github.com/Darwish-md/TryHackMe/assets/72353586/c663e508-6a37-4b75-86cc-9e384233169a)

#### What is NTLM?
- In a Windows network, NT (New Technology) LAN Manager (NTLM) is a suite of Microsoft security protocols intended to provide authentication, integrity, and confidentiality to users.
- Kerberos is the default authentication service for Microsoft Windows domains. It is intended to be more "secure" than NTLM by using third party ticket authorization as well as stronger encryption.

### Common Terminology
- Ticket Granting Ticket (TGT) - is an authentication ticket used to request service tickets from the TGS for specific resources from the domain.
- Key Distribution Center (KDC) - is a service for issuing TGTs and service tickets that consist of the ***Authentication Service*** and the ***Ticket Granting Service***.
  - Authentication Service (AS) - The Authentication Service ***issues TGTs*** to be used by the TGS in the domain to request access to other machines and service tickets.
  - Ticket Granting Service (TGS) - The Ticket Granting Service takes the TGT and ***returns a ticket*** to a machine on the domain.
- Service Principal Name (SPN) - is an identifier given to a service instance to associate a service instance with a domain service account. Windows requires that services have a domain service account which is why a service needs an SPN set.
- KDC Long Term Secret Key (KDC LT Key) - The KDC key is based on the KRBTGT service account. It is used to encrypt the TGT and sign the PAC.
- Client Long Term Secret Key (Client LT Key) - is based on the computer or service account. It is used to check the encrypted timestamp and encrypt the session key.
- Service Long Term Secret Key (Service LT Key) - is based on the service account. It is used to encrypt the service portion of the service ticket and sign the PAC.
- Session Key - Issued by the KDC when a TGT is issued. The user will provide the session key to the KDC along with the TGT when requesting a service ticket.
- Privilege Attribute Certificate (PAC) - The PAC holds all of the user's relevant information, it is sent along with the TGT to the KDC to be signed by the Target LT Key and the KDC LT Key in order to validate the user.

#### AS-REQ w/ Pre-Authentication In Detail (Granting TGTs & session key)
The AS-REQ step in Kerberos authentication starts when a user requests a TGT from the KDC. In order to validate the user and create a TGT for the user, the KDC must follow these exact steps. 
1. The first step is for the user to encrypt a timestamp NT hash and send it to the AS.
2. The KDC attempts to decrypt the timestamp using the NT hash from the user.
3. If successful the KDC will issue a TGT as well as a session key for the user.

#### TGT contents
The TGT is provided by the user to the KDC, in return, the KDC validates the TGT and returns a service ticket.

![image](https://github.com/Darwish-md/TryHackMe/assets/72353586/15b3c71a-ef35-4ed4-8ae6-589b314f06c3)

#### Service Ticket Contents 
A service ticket contains two portions: the service provided portion and the user-provided portion:
- Service Portion: User Details, Session Key, Encrypts the ticket with the service account NTLM hash.
- User Portion: Validity Timestamp, Session Key, Encrypts with the TGT session key.

![image](https://github.com/Darwish-md/TryHackMe/assets/72353586/189bcb9c-3ade-4481-adf9-18db7ac583e5)

#### To conclude the process (refer to the first pic)
- AS-REQ - 1.) The client requests an Authentication Ticket or Ticket Granting Ticket (TGT).
- AS-REP - 2.) The Key Distribution Center verifies the client and sends back an encrypted TGT.
- TGS-REQ - 3.) The client sends the encrypted TGT to the Ticket Granting Server (TGS) with the Service Principal Name (SPN) of the service the client wants to access.
- TGS-REP - 4.) The Key Distribution Center (KDC) verifies the TGT of the user and that the user has access to the service, then sends a valid session key for the service to the client.
- AP-REQ - 5.) The client requests the service and sends the valid session key to prove the user has access.
- AP-REP - 6.) The service grants access

### Different Attaks
#### Enumerating with Kerbrute
`./kerbrute_linux_amd64 userenum --dc <DOMAIN_CONTROLLER_IP> -d <DOMAIN_NAME> <WORDLIST_FILE>` will brute force user accounts from a domain controller using a supplied wordlist. 

Ex: `./kerbrute userenum --dc CONTROLLER.local -d CONTROLLER.local User.txt` (we added the IP of domain name to the DNS in `/etc/hosts`).

#### Rubeus
Rubeus has a wide variety of attacks and features that allow it to be a very versatile tool for attacking Kerberos. Just some of the many tools and attacks include overpass the hash, ticket requests and renewals, ticket management, ticket extraction, harvesting, pass the ticket, AS-REP Roasting, and Kerberoasting.

Exs:
1. `Rubeus.exe harvest /interval:30` - This command tells Rubeus to harvest for TGTs every 30 seconds.
2. `Rubeus.exe brute /password:Password1 /noticket` - This will take a given password and "spray" it against all found users then give the .kirbi TGT for that user.

#### 1. Kerberoasting
Kerberoasting allows a user to request a service ticket for any service with a registered SPN then use that ticket to crack the service password.

##### Steps in a Kerberoasting Attack:
I. Initial Access:
The attacker has a valid domain user account (even a low-privileged account). This allows them to interact with Active Directory.

II. SPN Lookup:
Every service running on an Active Directory domain has a Service Principal Name (SPN) associated with it. An attacker can query the domain to retrieve a list of SPNs, which are linked to service accounts.
Tools like PowerView or SetSPN can be used to enumerate SPNs in the domain.

III. Requesting the TGS:
The attacker uses their legitimate user account to request a Kerberos service ticket (TGS) for the identified SPN.
When this request is made, the Key Distribution Center (KDC) responds with a TGS encrypted using the service account's password hash (specifically using an NTLM or RC4 encryption algorithm based on the service account's password).

IV. Ticket Extraction:
The attacker extracts the TGS from memory. This ticket contains the encrypted portion which uses the service account's password hash as the key for encryption.

V. Offline Cracking:
Since the attacker doesn't know the password, they take the encrypted TGS and use password cracking tools to brute force or perform dictionary attacks to recover the plaintext password from the encrypted ticket.

##### What can be done with a service account?
- Exfiltrate Data or Collect Loot:
  - If the service account is a domain admin, you gain extensive control similar to a golden/silver ticket attack. This allows you to gather loot such as dumping the NTDS.dit, which contains hashed passwords of all users in the Active Directory domain.
  - If the service account is not a domain admin, you can still use it to log into other systems, pivot, or escalate privileges.
- Use Cracked Password for Further Attacks:
  - The cracked password can be used to spray against other service and domain admin accounts. Many companies may reuse the same or similar passwords for these accounts, allowing for further compromise.

##### How?
1. Using ***Rubeus***:
`Rubeus.exe kerberoast` - This will dump the Kerberos hash of any kerberoastable users. Then we use hashcat.

2. Using ***Impacket***:
`sudo python3 GetUserSPNs.py controller.local/Machine1:Password1 -dc-ip 10.10.79.92 -request` - This will dump the Kerberos hash for all kerberoastable accounts it can find on the target domain just like Rubeus does; however, this does not have to be on the targets machine and can be done remotely.

##### Kerberoasting Mitigation
- Strong Service Passwords.
- Don't Make Service Accounts Domain Admins - Service accounts don't need to be domain admins.

#### 2. AS/REP Roasting
AS-REP Roasting, similar to Kerberoasting, extracts krbasrep5 hashes of user accounts with Kerberos pre-authentication disabled. Unlike Kerberoasting, these users don't need to be service accounts; any user with pre-authentication disabled can be targeted. 

##### Normally
When pre-authentication is enabled, a user's hash encrypts a timestamp during authentication, which the domain controller decrypts to verify the hash's freshness and prevent replay attacks. 
##### what's different?
With pre-authentication disabled, requesting authentication data for any user returns an encrypted TGT without verifying their identity, making it susceptible to offline cracking.
##### How can we do it?
We can use Rubeus for AS/REP roasting: `Rubeus.exe asreproast` - This will run the AS-REP roast command [1] looking for vulnerable users and [2] then dump found vulnerable user hashes.

##### AS-REP Roasting Mitigations
- Have a strong password policy.
- Don't turn off Kerberos Pre-Authentication unless it's necessary there's almost no other way to completely mitigate this attack other than keeping Pre-Authentication on.
  
#### 3. Pass the ticket
- The Local Security Authority Subsystem Service (LSASS) is a memory process that stores credentials on an active directory server and can store Kerberos ticket along with other credential types to act as the gatekeeper and accept or reject the credentials provided. 
- Pass the ticket works by dumping the TGT from the LSASS memory of the machine.
- When you dump the tickets with mimikatz it will give us a .kirbi ticket which can be used to gain domain admin if a domain admin ticket is in the LSASS memory.
- Mimikatz can be simply used to dump tickets in memory, with the right privileges.
- domain admins SHOULD NOT log onto anything EXCEPT the domain controller - This is something so simple however a lot of domain admins still log onto low-level computers leaving tickets around that we can use to attack and move laterally with.

![image](https://github.com/Darwish-md/TryHackMe/assets/72353586/66443892-8d25-44e1-b7dd-0c9baa709919)

#### 4. Golden/Silver Ticket Attack with Mimikatz
- The key difference between the two tickets is that a silver ticket is limited to the service that is targeted whereas a golden ticket has access to any Kerberos service.
- If stealth and staying undetected matter then a silver ticket is probably a better option than a golden ticket however the approach to creating one is the exact same.
-  A ***KRBTGT*** is the service account for the KDC this is the Key Distribution Center that issues all of the tickets to the clients. If you impersonate this account and create a golden ticket form the KRBTGT you give yourself the ability to create a service ticket for anything you want.

##### Golden/Silver Ticket Attack Overview 
A Golden/Silver Ticket Attack involves dumping the ticket-granting ticket (TGT) of a user on the domain, preferably a domain admin for a golden ticket or any service/domain admin ticket for a silver ticket. This provides the attacker with the user's SID (security identifier) and NTLM hash. These details are then used in a mimikatz attack to create a TGT that impersonates the targeted service/domain admin account.

#### How?
In Mimikatz, we can use `lsadump::lsa /inject /name:krbtgt` to get the SID and the NTLM hash. Then `Kerberos::golden /user:Administrator /domain:controller.local /sid:<SID> /krbtgt:<NTLM Hash of krbtgt> /id:<ID>` can be used to create a golden ticket.

#### 5. Kerberos Backdoor w Mimikatz
The Kerberos backdoor works by implanting a skeleton key that abuses the way that the AS-REQ validates encrypted timestamps. A skeleton key only works using Kerberos RC4 encryption. 

The default hash for a mimikatz skeleton key is 60BA4FCADC466C7A033C178194C03DF6 which makes the password -"mimikatz"

The skeleton key works by abusing the AS-REQ encrypted timestamps, the timestamp is encrypted with the users NT hash. The domain controller then tries to decrypt this timestamp with the users NT hash, once a skeleton key is implanted the domain controller tries to decrypt the timestamp using both the user NT hash and the skeleton key NT hash allowing you access to the domain forest.
