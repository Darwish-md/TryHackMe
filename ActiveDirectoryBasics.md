- The main idea behind a domain is to centralise the administration of common components of a Windows computer network in a single repository called ***Active Directory (AD)***. 
- The server that runs the Active Directory services is known as a ***Domain Controller (DC)***.
- ***Active Directory Domain Service (AD DS)*** acts as a catalogue that holds the information of all of the "objects" that exist on your network. Amongst the many objects supported by AD, we have users, groups, machines, printers, shares and many others.
- security principals mean that they can be authenticated by the domain and can be assigned privileges over resources like files or printers.

### Difference between Organizational Unit and a Group in Active Directory:
- OUs are handy for applying policies to users and computers, which include specific configurations that pertain to sets of users depending on their particular role in the enterprise. Remember, a user can only be a member of a single OU at a time, as it wouldn't make sense to try to apply two different sets of policies to a single user.
- Security Groups, on the other hand, are used to grant permissions over resources. For example, you will use groups if you want to allow some users to access a shared folder or network printer. A user can be a part of many groups, which is needed to grant access to multiple resources.

- The process of granting privileges to a user over some OU or other AD Object is called Delegation.
