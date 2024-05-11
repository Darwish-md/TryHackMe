# NAT/PAT/Proxy
## NAT/PAT
NAT and PAT are primarily used for managing the routing of traffic between a private network (often with private IP addresses) and the public internet. They help conserve public IP addresses and allow multiple devices within the private network to share a single public IP address. NAT/PAT is typically implemented at the network router or gateway.

## Proxy 
- A proxy is an intermediary server that acts as a bridge between a user's device and the internet, allowing the user to access online resources indirectly.

- Reverse Proxy: A reverse proxy, on the other hand, is deployed to improve security, load balancing, and application delivery. It sits between clients (e.g., web browsers) and backend servers (e.g., web application servers). The reverse proxy forwards client requests to the appropriate backend server and can provide features like SSL termination, content caching, and security filtering.

- Forward proxy sits between the user and the internet, forwarding requests from the user to the internet and returning responses. 

- In a typical setup, the NAT/PAT functionality is often handled by the network infrastructure, such as a router or firewall, while the reverse proxy server is placed in the DMZ (Demilitarized Zone) or a specific network segment to manage incoming traffic to web applications or services.

# Serverless computing
Often referred to as serverless cloud or serverless execution, is a cloud computing model where developers can build and run applications without the need to manage the underlying infrastructure, servers, or hardware. In this model, cloud providers automatically manage server provisioning, scaling, and resource allocation, allowing developers to focus solely on writing code for their applications. 

# Load Balancing Algorithms:
- Round robin load balancing sends each client app request to the next backend server.
- Weighted load balancing uses a configured relative weight value for each backend server to determine how much traffic each server gets.
- Active/passive is a load balancing redundancy configuration where a standby server is not active until the active server fails.
- Least connections send client app requests to the backend server that is currently the least busy.

# Captive portal
presents a Web page when users connect to a Wi-Fi network; sometimes a user account is required (often users must agree to the terms of use before connecting to the Internet). 

# IaaS/SaaS/SECaaS/PaaS
- Infrastructure as a Service (IaaS) includes storage, network and virtual machines. IaaS virtual machine software patching is the responsibility of the cloud tenant.
- Software as a Service (SaaS) refers to end-user productivity software running in the cloud.
- Security as a Service (SECaaS) refers to cloud security services.
- Platform as a Service (PaaS) refers to database and software development platforms, all of which do not place the responsibility of virtual machine patching on the cloud tenant.

# Cloud Access Security Broker (CASB) 
It sits between users and cloud services to enforce organizational security policies. 

# Air gapping 
It is a strategy used to protect sensitive or critical computer systems and networks by physically isolating them from unsecured networks or the internet. In an air-gapped environment, there is no direct or networked connection between the isolated system (or systems) and external networks, which helps reduce the risk of cyberattacks and data breaches. 

# WMI 
Windows Management Instrumentation is an administration feature that provides a uniform environment to access Windows system components. The WMI service enables both local and remote access, though the latter is facilitated by Remote Services such as Distributed Component Object Model (DCOM) and Windows Remote Management (WinRM).

# BITS
Windows Background Intelligent Transfer Service is a low-bandwidth, asynchronous file transfer mechanism exposed through Component Object Model (COM). BITS is commonly used by updaters, messengers, and other applications preferred to operate in the background (using available idle bandwidth) without interrupting other networked applications. 

# W32Time
The Windows Time service enables time synchronization across and within domains. W32Time time providers are responsible for retrieving time stamps from hardware/network resources and outputting these values to other network clients.

# LSA 
The Local Security Authority (LSA) is the main component responsible for local security policy and user authentication. The LSA includes multiple dynamic link libraries (DLLs) associated with various other security functions, all of which run in the context of the LSA Subsystem Service (LSASS) lsass.exe process.

# XDG 
XDG entries are configurations or metadata entries used in Linux and Unix-like operating systems to define and manage various aspects of the user environment, such as application menus, file associations, and desktop integration. XDG stands for "X Desktop Group," and it aims to provide standardized settings and conventions for desktop environments.

# Launch Agent and Launch Daemon
In macOS, Launch Agents and Launch Daemons are mechanisms for automatically starting and managing processes:
- ***Launch Agent***: These are user-specific and are associated with a particular user session. They run in the background and perform tasks on behalf of the user, such as launching applications or performing maintenance tasks. Launch Agents are stored in the `~/Library/LaunchAgents` directory.
- ***Launch Daemon***: These are system-wide daemons that run independently of user sessions. They manage system-level services and processes, such as network services or system maintenance tasks. Launch Daemons are stored in the `/Library/LaunchDaemons` directory.
  
# AppCert DLLs
Also known as Application Compatibility DLLs, are dynamic-link libraries (DLLs) in the Windows operating system that play a role in ensuring compatibility for applications. These DLLs are used to implement compatibility fixes for specific applications that may not function correctly on newer versions of Windows.

# Application shimming
It is a technique used in Microsoft Windows operating systems to address compatibility issues between applications and the operating system. It allows legacy or incompatible applications to run on a newer version of Windows without modification to the application's source code.

# Emond 
Emond is a Launch Daemon that accepts events from various services, runs them through a simple rules engine, and takes action. The emond binary at `/sbin/emond` will load any rules from the `/etc/emond.d/rules/` directory and take action once an explicitly defined event takes place. The rule files are in the plist format and define the name, event type, and action to take. Some examples of event types include system startup and user authentication.

# KernelCallbackTable
Also known as the System Service Dispatch Table or SSDT (System Service Descriptor Table), is a data structure in the Windows operating system's kernel that contains function pointers to various system services (or functions). These services are essential for the functioning of the operating system, and they are called by applications and drivers when they need to perform privileged operations, such as file I/O or memory management.

# Horizontal/Vertical Bruteforce
- Horizontal: is similar to password spraying, where an attacker tries a few common passwords against many different user accounts simultaneously, hoping to gain unauthorized access by exploiting weak or commonly used passwords.
- Vertical brute force: focuses on trying multiple password combinations for a single user account, making it a more targeted approach.

# DOS/DDOS
A denial-of-service (DoS) attack floods a server with traffic, making a website or resource unavailable. A distributed denial-of-service (DDoS) attack is a DoS attack that uses multiple computers or machines (maybe controlled by one machine through bots or whatever) to flood a targeted resource.

# Process Hollowing
Process hollowing is a technique used by malware to inject malicious code into a legitimate process while maintaining the appearance of normal behavior. Here's how it works:
1. Create Suspended Process: The malware creates a new instance of a legitimate process (e.g., explorer.exe) in a suspended state. This process serves as the target for the injection.
2. Replace Memory Contents: The malware unmaps the memory of the legitimate process and replaces it with its malicious code. This effectively "hollows out" the legitimate process, leaving only the basic process structure intact.
3. Resume Process Execution: Once the malicious code is injected, the malware resumes execution of the legitimate process. From the outside, the process appears to be running normally, but it is actually executing the injected malicious code.
   
# NSG
A network security group in Azure is the way to activate a rule or access control list (ACL), which will allow or deny network traffic to your virtual machine instances in a virtual network. 

Unlike Azure Firewall, which monitors all traffic for workloads, NSG is commonly deployed for individual vNets, subnets, and network interfaces for virtual machines to refine traffic. It does so by activating a rule (allow or deny) or Access Control List (ACL), which allows or denies traffic to Azure resources.

# Fileless malware
It is malicious code that works directly within a computer's memory instead of the hard drive. It uses legitimate programs to compromise your computer instead of malicious files (Injecting code into an existing legitimate software). These attacks can be detected only with memory based forensic techniques

# Cyber threat intelligence (CTI)
It consists of information related to cyber threats and threat actors. It incorporates various sources to help identify and mitigate harmful events and potential attacks occurring in cyberspace.
- Most utilized form of CTI is threat indicators IoCs.
- Threat indicators are data that associates observations URLs, file hashes or IP addresses.

# Rootkit 
is a type of malicious software designed to gain unauthorized access to a computer system while hiding its presence and activities from users and security mechanisms. It is called a "rootkit" because it typically targets the "root" or core of a system, aiming to obtain elevated privileges and control over the system.

# RAT
A Remote Access Trojan (RAT) is a type of malware that enables attackers to remotely control infected computers or devices. After infecting a system, the RAT establishes a connection with the attacker's command-and-control server, allowing them to execute commands, steal data, and conduct various malicious activities.

# Drive-by download/compromise
- Drive-by Compromise: adversaries exploit vulnerabilities in web browsers, often by injecting malicious code into legitimate websites or modifying script files served from public cloud storage. When users visit these compromised sites, their browsers may be exploited, enabling attackers to gain unauthorized access to their systems. Besides direct exploitation, adversaries might also use compromised websites for other malicious activities, such as acquiring Application Access Tokens, posing a significant threat to users' cybersecurity during routine web browsing.

- Drive-by download: is a type of cyberattack where malicious software is downloaded and installed on a user's device without their knowledge or consent. Drive-by downloads exploit vulnerabilities in web browsers, plugins, or operating systems, allowing attackers to deliver malware, such as viruses, ransomware, or Trojans, without the user's interaction.

- These attacks are particularly dangerous because they can happen without any action from the user, apart from simply visiting a compromised website.
  
# A QNAP NAS 
It is a powerful device that allows you to store and share files and access them from anywhere in the world. You can use it for work, school, or at home. A QNAP NAS device can also be accessed by multiple users simultaneously, making it ideal for small businesses or teams working on large projects.

# Present Threats:
## Emotet:
- Emotet was originally designed as a banking malware that attempted to sneak onto your computer and steal sensitive and private information.
- Emotet has gone through a few iterations. Early versions arrived as a malicious JavaScript file. Later versions evolved to use macro-enabled documents to retrieve the virus payload from command and control (C&C) servers run by the attackers. 
-  Emotet knows if it’s running inside a virtual machine (VM) and will lay dormant if it detects a sandbox environment, which is a tool cybersecurity researchers use to observe malware within a safe, controlled space.
- Emotet also uses C&C servers to receive updates. This works in the same way as the operating system updates on your PC and can happen seamlessly and without any outward signs. 
-The primary distribution method for Emotet is through malspam. Emotet ransacks your contacts list and sends itself to your friends, family, coworkers and clients. 
- If a connected network is present, Emotet spreads using a list of common passwords, guessing its way onto other connected systems in a brute-force ­attack.
-  It has been used to deliver a range of malicious payloads, including ransomware and other banking Trojans, making it a significant threat to individuals, organizations, and even governments.
- How to protect? - Don't download or click suspicious entities. - update endpoints - educate yourself and employess.
- It was discovered in 2014

## SocGholish:
- it is an attack framework that leverages drive-by downloads masquerading as legitimate software (browser) update like "AutoUpdater.js"
- it has been out there since 2018
- SocGholish is delivered via injected JavaScript on compromised websites.
- SocGholish, while relatively easy to detect, is difficult to stop.
- Threat Research has observed SocGholish being leveraged in email campaigns with injections on sites that meet one of two criteria:
  1- Extensive marketing and legitimate email advertising campaigns.
  2- Strong SEO (Search Engine Optimization) and page rank causing aggregation and dissemination by Google Alerts and other similar services.
- so Basically, it doesn't mainly spread via email, but more via aggregate service (Google alerts), marketing services.
- SocGholish has 3 stages:
	1. Initial Compromise:
SocGholish initiates with a "drive-by" download technique. Malicious JavaScript is injected into compromised legitimate websites. When an unsuspecting victim clicks on a link from an email leading to a compromised site, the injected JavaScript executes upon the browser loading the page. Eligible victims (using Windows, external sources, and specific cookie checks) are presented with a download link masquerading as a browser update.

	2. Download and Execution:
Upon meeting specific eligibility criteria, users are prompted to download and execute a file, often disguised as a browser update. Additional eligibility checks are performed, and upon approval, a compressed archive containing a JavaScript file (e.g., "AutoUpdater.js") is served. When the user executes this payload, the second stage begins.

	3. System Profiling and Data Exfiltration:
In the third stage, the malicious JavaScript payload invokes Windows Management Instrumentation (WMI) calls, often using native Windows script hosts like WScript or CScript. These calls profile the system, gathering data such as domain trusts, usernames, and computer names. This information is then exfiltrated to attacker-controlled infrastructure. This reconnaissance phase allows the attackers to assess the system further and avoid deploying their ultimate payload in environments where analysis might be conducted.


## USB Worms:
- USB worms are a type of malicious software that spreads through removable USB drives and other portable storage devices. 
- These worms exploit the autorun feature in Windows operating systems, allowing them to automatically execute and infect a computer when the infected USB drive is connected to it. Once the worm gains access to the system, it can replicate itself onto the computer's hard drive, other connected USB drives, and even network drives if available.
- USB worms can carry a variety of payloads, including viruses, Trojans, or other types of malware. 
- They can cause significant damage by corrupting files, stealing sensitive information, disrupting system functions, or enabling remote control of the infected computer.

EXAMPLE: Raspberry Robin
- First spotted in September 2021, it was typically introduced into a network through infected removable drives, often USB devices.
- Initially, the Raspberry Robin worm often appears as a shortcut .lnk file masquerading as a legitimate folder on the infected USB device. The name of the lnk file was recovery.lnk which later changed to filenames associated with the brand of the USB device. 
- Raspberry Robin uses both autoruns to launch and social engineering to encourage users to click the LNK file.
- Raspberry Robin’s LNK file points to cmd.exe to launch the Windows Installer service msiexec.exe and install a malicious payload hosted on compromised QNAP network attached storage (NAS) devices.
- Raspberry Robin gains persistence by adding itself to the RunOnce key in the CurrentUser registry hive of the user who executed the initial malware.
- In Windows, the autorun of USB drives is disabled by default. However, many organizations have widely enabled it through legacy Group Policy changes.

## WannaCry Ransomeware
this nasty worm was spread via an operation that hunts down vulnerable public facing SMB ports and then uses the alleged NSA-leaked EternalBlue exploit to get on the network and then the (also NSA alleged) DoublePulsar exploit to establish persistence and allow for the installation of the WannaCry Ransomware.

[1] w3wp.exe
- w3wp.exe is a process associated with Microsoft Internet Information Services (IIS), which is a web server software for Windows Server systems. 
- When a user accesses a website hosted on a server running IIS, the w3wp.exe process is responsible for handling the web application requests. Each IIS application pool runs in its own w3wp.exe process. This isolation helps in maintaining the stability and security of the web server. If a particular web application experiences issues, it won't affect other applications because they are running in separate processes.

Understanding w3wp.exe:

- Process Name: w3wp.exe stands for Windows Web Worker Process. It's a user-mode process that runs web applications in IIS (Internet Information Services) on Windows Server operating systems.
- Application Pool Isolation: In IIS, web applications are grouped into application pools. Each application pool runs in its own w3wp.exe process. This isolation ensures that if one application encounters issues (e.g., memory leaks or crashes), it won't directly affect other applications running on the same server.
- Role: The w3wp.exe process handles incoming HTTP requests, processes ASP.NET pages, manages sessions, and ensures the proper execution of web applications hosted on the server.

Security Issues and Vulnerabilities:
a. Denial-of-Service (DoS) Attacks:
    Resource Exhaustion: Attackers can attempt to overload the server with a large number of requests, causing the w3wp.exe processes to consume excessive CPU and memory resources, leading to system slowdown or unresponsiveness.

b. Remote Code Execution (RCE):
    Vulnerabilities in Web Applications: If a web application running within IIS has security vulnerabilities (like SQL injection or unvalidated input), attackers might exploit these to execute arbitrary code, potentially taking control of the server.

c. Unauthorized Access:
    Weak Authentication: If authentication mechanisms are not properly configured, unauthorized users might gain access to sensitive parts of the web application.

d. Information Disclosure:
    Error Messages: Improperly configured error handling might reveal sensitive information, such as stack traces or database connection details, which could aid attackers in crafting more precise attacks.

e. Insecure Direct Object References (IDOR):
    Insecure File Access: If file permissions are not properly configured, attackers could potentially access files or directories outside the web application's scope.

f. DDoS Amplification:
    Open Endpoints: Certain endpoints might be abused for DDoS amplification attacks, where small requests trigger large responses, leading to a bandwidth-fueled DDoS attack.

-------------------------------
Malware static and dynamic analysis:

1. Static Analysis:

Static analysis involves examining the malware without executing it. Analysts dissect the malware code, structure, and characteristics to gain insights into its functionality. Here are the key aspects of static analysis:

    File Signature Analysis: Malware files often have unique signatures. Antivirus programs use these signatures to identify known malware.

    Code Disassembly: Malware code can be disassembled or decompiled to understand its logic and functionality.

    Behavioral Analysis: Analysts examine the code to identify potential malicious behavior, such as file modification, registry changes, or network communications.

    String Analysis: Strings within the malware, such as URLs, IP addresses, or encryption keys, provide valuable clues about its purpose and origin.

    Packers and Obfuscation: Malware authors often use packers or obfuscation techniques to hide the true nature of their code. Static analysis can involve unpacking and deobfuscating the code to reveal its original form.

    Resource Examination: Malware binaries can contain embedded resources like images or configuration files, providing additional context.

2. Dynamic Analysis: (ANY.RUN, hybrid analysis)

Dynamic analysis involves executing the malware in a controlled environment (like a sandbox) and observing its behavior in real-time. Here are the key aspects of dynamic analysis:

    Behavior Monitoring: Analysts observe how the malware behaves when executed, including its interactions with the file system, registry, network, and other system resources.

    Network Traffic Analysis: Dynamic analysis can reveal network communications initiated by the malware, including command and control (C&C) server communications.

    System Calls and API Monitoring: Analysts monitor system calls and API (Application Programming Interface) interactions to understand what actions the malware is attempting to perform on the host system.

    Code and Memory Analysis: Dynamic analysis can involve runtime debugging, allowing analysts to inspect the code and memory while the malware is running.

Comparison:

    Static Analysis Pros:
        Safer: Since it doesn't involve executing the malware, static analysis is safe and doesn't risk further infection.
        Faster: Static analysis is generally quicker than dynamic analysis.
        No Sandbox Evasion: Malware might detect virtual environments and behave differently. Static analysis doesn't have this limitation.

    Dynamic Analysis Pros:
        Real Behavior: Dynamic analysis provides insights into the actual behavior of the malware, including its evasion techniques and encryption keys.
        Interaction with External Entities: Observing network communications and interactions with external servers is possible only in dynamic analysis.
        Unpack Obfuscated Code: Dynamic analysis allows the study of unpacked, deobfuscated code when the malware is executed.
-------------------------------
persistence refers to a malware's ability to remain on a system across reboots or system shutdowns. One common way malware achieves persistence is by creating entries in the Windows Registry. The Windows Registry is a hierarchical database used by the Windows operating system to store configuration data for the system, applications, and users.

Malware can add registry entries to ensure that it runs every time the system starts. These entries are often added to specific registry keys, such as the "Run" or "RunOnce" keys, which are automatically executed by the operating system during the startup process.

IN SHORT:
Persistence, when talking about technique T1547.001, is the modification of specific registry keys and values in order to have an executable, command, or script run every time the system is rebooted. 
---------------------------------
the "Autostart catalog" typically refers to specific locations in the Windows Registry and filesystem where information about programs that are configured to start automatically with the operating system is stored. 

Registry Locations:
1. `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run`: Programs listed here run automatically when a specific user logs in.

    HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run:
    Programs listed here run automatically when any user logs in.

    HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce:
    Programs listed here run once when a specific user logs in.

    HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunOnce:
    Programs listed here run once when any user logs in.
	
Filesystem Locations:

    Startup Folder (Per-User):
    %APPDATA%\Microsoft\Windows\Start Menu\Programs\Startup
    Programs or shortcuts placed here run when a specific user logs in.

    Startup Folder (All Users):
    %ALLUSERSPROFILE%\Microsoft\Windows\Start Menu\Programs\Startup
    Programs or shortcuts placed here run when any user logs in.
	
Why Monitoring Autostart Entries is Important:

    Malware Persistence: Malware often adds entries in these locations to ensure it runs every time the system starts, making it crucial to monitor these locations for suspicious entries.

    System Performance: Unnecessary programs in the autostart can slow down the system startup process, affecting overall performance.

    Security: Malicious programs in the autostart can compromise system security and lead to unauthorized access or data theft.
------------------------------
Cyber Kill chain: A series of steps that describe the progression of a cyber attack from reconnaissance all the way to exfiltration
- Developed by Lockheed Martin, the Cyber Kill Chain provides a framework for understanding and countering advanced persistent threats.
- The term "kill chain" comes from military terminology, where it refers to the structure of an attack, from identifying the target to the destruction of the target.

Stages:
    Reconnaissance: Attackers gather information about the target, often using publicly available data, social engineering, or scanning tools to identify potential vulnerabilities and targets within the organization.

    Weaponization: Attackers create or obtain malicious software, exploits, or other tools that can be used to compromise systems. This stage involves turning the identified vulnerabilities into functional weapons.

    Delivery: Attackers deliver the weaponized payload to the target. This can occur through emails with malicious attachments, infected websites, or other means that trick users into activating the malware.

    Exploitation: The malicious payload is executed, taking advantage of vulnerabilities to gain unauthorized access, escalate privileges, or execute specific commands on the target system.

    Installation: The malware is installed on the compromised system. This often involves establishing persistence mechanisms, ensuring the malware remains active even after system reboots, and setting up communication channels with remote servers controlled by the attackers.

    Command and Control (C2): The attacker establishes a connection to the compromised system, allowing them to send commands and receive data. This stage enables remote control and coordination of the compromised devices.

    Actions on Objectives: The attackers carry out their ultimate goals, which could involve data theft, financial fraud, disrupting operations, or any other malicious activities as per their objectives.
------------------------------------
- The 3CX Desktop App is a Voice over Internet Protocol (VoIP) type of application which is available for Windows, macOS, Linux and mobile. Many large corporations use it internally to make calls, view the status of colleagues, chat, host web conferences, and for voicemail. 3CX is a Private Branch Exchange (PBX) system, which is basically a private telephone network used within a company or organization.
-  It is likely the attacks have been ongoing since one of the shared samples was digitally signed on March 3, 2023, with a legitimate 3CX Ltd certificate issued by DigiCert.
- While it is almost certain that Windows Electron clients are affected, there is no evidence so far that any other platforms are. On the 3CX forums, users are being told that only the new version (3CX Desktop App) leads to the malware infection, because the 3CX Phone for Windows (the legacy version) is not based on the Electron Framework. Electron is an open source project that enables web developers to create desktop applications.
- The main executable is not malicious itself and can be downloaded from 3CX's website as part of an installation procedure or an update. The 3CXDesktopApp.exe executable, however, sideloads a malicious dynamic link library (DLL) called ffmpeg.dll.
- The ffmpeg.dll in turn is used to extract an encrypted payload from d3dcompiler_47.dll and execute it. The malware then downloads icon files hosted on GitHub that contain Base64 encoded strings appended to the end of the images.
------------------------------------
# Threat campaign
It is a coordinated series of malicious activities orchestrated by threat actors with specific objectives. These objectives could include stealing sensitive data, disrupting operations, causing financial losses, or gaining unauthorized access to systems. Threat campaigns are typically well-organized, targeted, and often involve multiple attack vectors.

### IN SHORT:
An individual or group involved in malicious cyber activity is called a Threat Actor. A set of activity (Incidents) carried out by Threat Actors using specific techniques (TTP) [tactics, techniques, and procedures] for some particular purpose is called a Campaign.

### Characteristics of threat campaign:

1. Organized Effort: Threat campaigns are not random attacks. They involve careful planning, organization, and coordination among threat actors. Multiple individuals or groups might be involved, each specializing in different aspects of the attack.

2. Specific Objectives: Threat campaigns have clear goals. These objectives could vary, such as stealing intellectual property, conducting espionage, launching DDoS (Distributed Denial of Service) attacks, or disrupting critical infrastructure.

3. Persistence: Threat campaigns are ongoing and persistent. Attackers continuously adapt their tactics, techniques, and procedures (TTPs) to evade detection, maintain access, and achieve their goals over an extended period.

4. Targeted Victims: Threat campaigns often target specific individuals, organizations, industries, or regions. Attackers conduct thorough reconnaissance to identify vulnerable targets that align with their objectives.

5. Multifaceted Attacks: Threat campaigns employ multiple attack vectors and techniques. These can include phishing emails, malware infections, social engineering, zero-day exploits, supply chain attacks, and more. The combination of tactics makes them harder to detect and defend against.

6. Advanced Tools: Threat actors often use sophisticated tools and malware, including custom-designed software, to exploit vulnerabilities and gain unauthorized access to systems. These tools are continually updated and customized for specific targets.

7. Evasion Techniques: Threat campaigns employ evasion techniques to bypass security measures. This includes polymorphic malware, encryption, anti-analysis methods, and anti-forensic techniques to make it difficult for cybersecurity professionals to analyze and detect their activities.

# STIX
Structured Threat Information eXpression is a standardized XML programming language for conveying data about cybersecurity threats in a common language that can be easily understood by humans and security technologies. Designed for broad use, there are several core use cases for STIX.

# Kerberos delegation
Kerberos delegation is a feature in the Kerberos authentication protocol that allows a service to impersonate a user and access other network resources on behalf of that user. 

When the user accesses a service that supports delegation, the service can request a service ticket on behalf of the user for another service (referred to as the target service) using the TGT.

# Registry Hive
A hive is a logical group of keys, subkeys, and values in the registry that has a set of supporting files loaded into memory when the operating system is started or a user logs in.

For example, each time a new user logs on to a computer, a new hive is created for that user with a separate file for the user profile. This is called the user profile hive. A user's hive contains specific registry information pertaining to the user's application settings, desktop, environment, network connections, and printers.

# COM Hijacking
COM hijacking is a technique used by attackers to take advantage of the Component Object Model (COM) infrastructure in Windows systems. Here's a brief overview:

### COM Infrastructure 
COM is a Microsoft technology that enables inter-process communication and allows software components to interact with each other. It is widely used in Windows for various purposes, including automation, inter-process communication, and object-oriented programming.

### Hijacking Technique
In COM hijacking, attackers exploit insecure configurations or vulnerabilities in the Windows registry or file system to redirect the loading of COM objects. By manipulating registry settings or placing malicious DLL files in specific locations, attackers can trick legitimate applications into loading and executing their malicious code instead of the intended COM objects.

Execution of Malicious Code: Once the COM object is hijacked, the attacker's malicious code is executed within the context of the legitimate application or process, allowing them to carry out various malicious activities, such as stealing sensitive information, executing arbitrary commands, or compromising the system's security.

# DLL Redirection:
The SysWOW64 directory on 64-bit versions of Windows contains 32-bit system files, while the System32 directory contains 64-bit system files. If a 32-bit application running under the SysWOW64 directory attempts to load a DLL that does not exist in the SysWOW64 directory but exists in the System32 directory, Windows may redirect the request to the System32 directory. This redirection could result in C:\Windows\SysWOW64\rundll32.exe spawning C:\Windows\System32\rundll32.exe as part of normal system behavior.

# Dropper attack
is a cyberattack where malware is delivered onto a victim's system through a malicious program called a dropper. The dropper, disguised as a legitimate file or application, is delivered via email, phishing links, or compromised websites. Once executed, the dropper installs and executes the malware payload, allowing attackers to carry out malicious activities.

# Portable executable PE:
 A file format for executables, object code, DLLs, FON Font files, and others used in 32-bit and 64-bit versions of Windows operating systems. The PE format is a data structure that encapsulates the information necessary for the Windows OS to manage the wrapped executable code.

# software packing
Legitimate software developers use packing to reduce the size of their applications and to ultimately protect their work from being stolen. It is, however, a double-edged sword, malware authors reap the benefits of packing to make the reverse engineering and detection of the code hard to impossible.

Packed files have a few characteristics that may indicate whether or not they are packed:
- Packed files will have a high entropy!
- There are very few "Imports", packed files may only have "GetProcAddress" and "LoadLibrary".
- The executable may have sections named after certain packers such as UPX.
- When an executable is packed, it must unpack itself before any code can execute. Because of this, packers change the entry point from the original location to what's called the "Unpacking Stub".

# Homograph attacks 
They involve creating web addresses that visually resemble legitimate ones by using characters from different scripts, aiming to deceive users into visiting malicious sites. For instance, the English word "apple" might be represented as "аррӏе.com" where the first and last characters are Cyrillic characters that visually resemble the Latin letters "a" and "e". 

# Stateful vs Stateless Firewalls
- A stateful firewall keeps track of the state of active connections, allowing it to make decisions based on the context of the traffic. It can discern between legitimate traffic and unauthorized access by analyzing the state of connections.
- On the other hand, a stateless firewall filters traffic based solely on predetermined criteria such as source and destination addresses, ports, and protocols. It doesn't maintain information about the state of connections, so each packet is evaluated in isolation without considering the context of the traffic flow.

# Side Notes: 
- The HTTPOnly flag ensures that client Javascript cannot access the cookie which can help mitigate cross-site scripting (XSS) attacks.
- The maximum proposed speed for 5G is 10 Gbps.
- Hashing algorithms don't typically use keys.
- Elliptic Curve Cryptography (ECC) uses small keys to achieve strong crypto strength.
- Geotagging adds geographic metadata (such as GPS coordinates) to files, such as photos taken with a smart phone.
- Geofencing uses geographical location to control app access.
- Side loading refers to installing mobile device apps directly from installation files, without using an app store.
- A content delivery network (CDN) is a group of geographically distributed servers that speed up the delivery of web content by bringing it closer to where users are.
  
-  A native API, short for Native Application Programming Interface, is a set of software functions and protocols provided by an operating system or platform to enable developers to create applications that are tightly integrated with and optimized for that specific system.
  
- Account manipulation may consist of any action that preserves adversary access to a compromised account, such as modifying credentials or permission groups. These actions could also include account activity designed to subvert security policies, such as performing iterative password updates to bypass password duration policies and preserve the life of compromised credentials.

- Active Setup is a feature in the Windows operating system that allows administrators to run specific commands or scripts when a user logs into the system for the first time. It's commonly used for tasks such as configuring user profiles, installing software components, or performing one-time setup actions. Active Setup ensures that these tasks are executed only once per user, typically during user login.

- Registry keys are elements within the Windows Registry database, which is stored in binary format on disk. They are organized in a hierarchical structure, similar to a tree, with keys and subkeys.

- Trap command allows programs and shells to specify commands that will be executed upon receiving interrupt signals. A common situation is a script allowing for graceful termination and handling of common keyboard interrupts like ctrl+c and ctrl+d.

- Tainted binaries refer to executable files or software programs that have been compromised or modified in a way that makes them untrustworthy or potentially malicious.

- user32.dll is a critical system file in Windows that enables graphical user interfaces (GUIs) and user interactions in applications. It manages windows, handles user input, and provides functions for creating GUI elements like buttons and menus. It's essential for the functionality of Windows-based software.

- A PowerShell profile (profile.ps1) is a script that runs when PowerShell starts and can be used as a logon script to customize user environments.

- Website defacement is an attack on a website that changes the visual appearance of a website or a web page.

- domain joined refers to a computer that is connected to a central server in a Windows domain network. 

- Domain squatters register domain names with the intent to profit from reselling them at a higher price. It involves registering domain names that closely resemble popular brands with the hope of capitalizing on the traffic or brand recognition associated with those names.

- A memory dump is a file containing all the information that was stored in RAM prior to a system failure that can be used to diagnose the cause of the crash.

- Entropy is the measure of randomness of data in a file. Entropy is very useful in identifying compressed and packed malware. Packed or compressed files usually have a high entropy.

- Threat Model: A risk assessment that models organizational strengths and weaknesses.

- An Intrusion Set is a grouped set of adversarial behaviors and resources with common properties that is believed to be orchestrated by a single organization.

# Windows Processes
1. 

2. Spoolsv
spoolsv.exe is a Windows system process responsible for managing print jobs and printer queues. It stands for "Spooler SubSystem App." This process handles the printing tasks on a Windows computer, ensuring that print jobs are sent to the appropriate printer and managed in an orderly fashion.


latest owasp

arp spoofing 

hashcat powershellempire, metasploit mimikatz 

ip ranges

common ports

credential injection attempt 

 position tech reqs
 
 Sudo !!
 
Use rustscan to discover open ports and then use nmap with open ports, saves tons of time
It is painfully slow using the attack box for me as well if using -p- but -A runs really quick on its own. I'm in the tail end of network services as well.
You can use -T5 to increase the speed of it.
nmap has a --min-rate flag where you can specify the minimum amount of packets to be sent per second. I find that 3-5,000pps is a pretty safe number, but it can always be adjusted as needed
nmap -sC -sV -A -T5 
-F -Pn -n
--packet-trace
