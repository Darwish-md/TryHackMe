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
AS-REQ - 1.) The client requests an Authentication Ticket or Ticket Granting Ticket (TGT).
AS-REP - 2.) The Key Distribution Center verifies the client and sends back an encrypted TGT.
TGS-REQ - 3.) The client sends the encrypted TGT to the Ticket Granting Server (TGS) with the Service Principal Name (SPN) of the service the client wants to access.
TGS-REP - 4.) The Key Distribution Center (KDC) verifies the TGT of the user and that the user has access to the service, then sends a valid session key for the service to the client.
AP-REQ - 5.) The client requests the service and sends the valid session key to prove the user has access.
AP-REP - 6.) The service grants access
