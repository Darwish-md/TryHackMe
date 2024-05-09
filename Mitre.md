# What is MITRE?
From Mitre.org: "At MITRE, we solve problems for a safer world. Through our federally funded R&D centers and public-private partnerships, we work across government to tackle challenges to the safety, stability, and well-being of our nation."

# Projects/research that the US-based non-profit MITRE Corporation has created for the cybersecurity community:
- ATT&CK® (Adversarial Tactics, Techniques, and Common Knowledge) Framework
- CAR (Cyber Analytics Repository) Knowledge Base
- ENGAGE
- D3FEND (Detection, Denial, and Disruption Framework Empowering Network Defense)
- AEP (ATT&CK Emulation Plans)

APT is an acronym for Advanced Persistent Threat. This can be considered a team/group (threat group), or even country (nation-state group), that engages in long-term attacks against organizations and/or countries.

Threat Model is a risk assessment that models organizational strengths and weaknesses

Emulation plans are a step-by-step guide on how to mimic the specific threat group.

##### TTP is an acronym for Tactics, Techniques, and Procedures
- The Tactic is the adversary's goal or objective.
- The Technique is how the adversary achieves the goal or objective.
- The Procedure is how the technique is executed.

## ATT&CK®
"MITRE ATT&CK® is a globally-accessible knowledge base of adversary tactics and techniques based on real-world observations."

In Enterprise version, we have 14 categories. Each category contains the techniques an adversary could use to perform the tactic. The categories cover the seven-stage Cyber Attack Lifecycle (credit Lockheed Martin for the Cyber Kill Chain).

### Tactics

#### 1. Reconnaissance	
The adversary is trying to gather information they can use to plan future operations.

##### Examples
1. ***Spearphishing***: a type of phishing attack that targets specific individuals or organizations in order to steal personal information that can lead to have access to an account, help attackers in the later procedures, etc

2. ***Search open websites/domains*** : Adversaries may search freely available websites and/or domains for information about victims that can be used during targeting. Information about victims may be available in various online sites, such as social media, new sites. it contains 3 sub-techniques which are [social media, search engines (google dorks for example), code repositories].

3. ***Search Closed Sources***: Adversaries may search and gather information about victims from closed sources such as dark web or cybercrime blackmarkets. They can also search private data from threat intelligence vendors. Although sensitive details such as customer names may be redacted, this information may contain trends regarding breaches such as target industries, attribution claims, and successful TTPs/countermeasures.
   
#### 2. Resource Development
The adversary is trying to establish resources they can use to support operations.

##### Examples
1. ***Acquire Access***: Adversaries may purchase or otherwise acquire an existing access to a target system or network. A variety of online services and initial access broker networks are available to sell access to previously compromised systems.

2. ***Obtain Capabilities***: Adversaries may buy and/or steal capabilities that can be used during targeting. Rather than developing their own capabilities in-house, adversaries may purchase, freely download, or steal them. Activities may include the acquisition of malware, software (including licenses), exploits, certificates, and information relating to vulnerabilities. sub-techniques include: [Malware, Tool, Exploits, Vulnerabilities]

3. ***Stage Capabilities***: Adversaries may upload, install, or otherwise set up capabilities that can be used during targeting. This can include:
  + Staging web resources necessary to conduct Drive-by Compromise when a user browses to a site.
  + Staging web resources for a link target to be used with spearphishing.
  + Uploading malware or tools to a location accessible to a victim network to enable Ingress tool transfer.
    
#### 3. Initial Access	
The adversary is trying to get into your network.

##### Examples
1. ***Content Injection***: Adversaries can gain access to victims by injecting malicious content into online network traffic, bypassing the need for victims to visit compromised websites. It can happen through content injection into DNS, HTTP, and SMB replies to targeted hosts that redirect them to download malicious files.

2. ***Drive-by Compromise***: Adversaries exploit vulnerabilities in web browsers, often by injecting malicious code into legitimate websites or modifying script files served from public cloud storage. When users visit these compromised sites, their browsers may be exploited, enabling attackers to gain unauthorized access to their systems (cross-site scripting). Besides direct exploitation, adversaries might also use compromised websites for other malicious activities, such as acquiring Application Access Tokens, posing a significant threat to users' cybersecurity during routine web browsing. 

3. ***Supply Chain Compromise***: Examples include:
  + Manipulation of development tools
  + Manipulation of a development environment
  + Manipulation of source code repositories (public or private)
  + Manipulation of source code in open-source dependencies
  + Manipulation of software update
    
4. ***Replication through Removable Media***: Adversaries may move onto systems, possibly those on disconnected or air-gapped networks, by copying malware to removable media and taking advantage of Autorun features when the media is inserted into a system and executes.
   
#### 4. Execution	
The adversary is trying to run malicious code.

##### Examples
1. ***Scheduled Task/Job***: Adversaries may abuse task scheduling functionality to facilitate initial or recurring execution of malicious code.

2. ***Serverless execution***: It refers to a cloud computing model where the cloud provider dynamically manages the allocation and scaling of resources needed to execute code. adversaries may use serverless functions to execute malicious code, such as crypto-mining malware.

3. ***Command and Scripting Interpreter***: Adversaries may abuse command and script interpreters to execute commands, scripts, or binaries. macOS and Linux distributions include some flavor of Unix Shell while Windows installations include the Windows Command Shell and PowerShell.

#### 5. Persistence	
The adversary is trying to maintain their foothold.

##### Examples
1. ***Create Account***

2. ***Boot or Logon Autostart Execution*** (Registry Keys and Startup Folders, or modifying any DLLs or scripts that are run on startup)

3. ***Hijack Execution Flow***: Adversaries may execute their own malicious payloads by hijacking the way operating systems run programs. This includes manipulating:
   + How the operating system locates programs to be executed.
   + How the operating system locates libraries to be used by a program can also be intercepted.
   + Locations where the operating system looks for programs/resources, such as file directories and in the case of Windows the Registry, could also be poisoned to include malicious payloads.

#### 6. Privilege Escalation
The adversary is trying to gain higher-level permissions. remember abou zero-logon that gives us the whole DC credentials.
   
##### Examples
1. ***Escape to Host***: In principle, containerized resources should provide a clear separation of application functionality and be isolated from the host environment. Adversaries may break out of a container to gain access to the underlying host. This can allow an adversary access to other containerized resources from the host level or to the host itself.

2. ***Access Token Manipulation***: An adversary can use built-in Windows API functions to copy access tokens from existing processes; this is known as token stealing. These tokens can then be applied to an existing process that needs higher privilege.

3. ***Account Manipulation***: Account manipulation is any action that preserves or modifies adversary access to a compromised account, such as modifying credentials or permission groups. For example adding created accounts to local admin groups.
   
#### 7. Defense Evasion
The adversary is trying to avoid being detected.

##### Examples
1. ***Process Injection***: Adversaries may inject code into processes in order to evade process-based defenses as well as possibly elevate privileges.
   + It allow access to the process's memory, system/network resources, and possibly elevated privileges.
   + It evades detection from security products since the execution is masked under a legitimate process.

2. ***Masquerading***: Adversaries may attempt to manipulate features of their artifacts to make them appear legitimate or benign. Masquerading occurs when the name or location of an object, legitimate or malicious, is manipulated or abused for the sake of evading defenses and observation. This can be like installing malicious tool which has a name of svchost.exe for example.

3. ***Rootkit***:  It is a type of malicious software designed to gain unauthorized access to a computer system while hiding its presence and activities from users and security mechanisms. It is called a "rootkit" because it typically targets the "root" or core of a system, aiming to obtain elevated privileges and control over the system.

4. ***Deobfuscate/Decode Files or Information***
   
#### 8. Credential Access
The adversary is trying to steal account names and passwords.

##### Examples
1. ***Bruteforce***
   
2. ***Adversary-in-the-Middle***: Adversaries may attempt to position themselves between two or more networked devices using an adversary-in-the-middle. For example, adversaries may manipulate victim DNS settings to enable other malicious activities such as preventing/redirecting users from accessing legitimate sites and/or pushing additional malware.

3. ***Input Capture***: Adversaries may use methods of capturing user input to obtain credentials or collect information like using a keylogger.

4. ***Steal Web Session Cookie or Kerberos Ticket*** 

5. ***OS Credential Dumping***: Adversaries may attempt to dump credentials to obtain account login and credential material, normally in the form of a hash or a clear text password. This can happen using tools like Mimikatz.

#### 9. Discovery
The adversary is trying to figure out your environment.

##### Examples
1. ***Browser Information Discovery***: Adversaries may enumerate information about browsers to learn more about compromised environments. Data saved by browsers (such as bookmarks, accounts, and browsing history) may reveal a variety of personal information about users (e.g., banking sites, relationships/interests, social media, etc.) as well as details about internal network resources such as servers, tools/dashboards, or other related infrastructure.

2. ***Process Discovery***: Adversaries may attempt to get information about running processes on a system. Information obtained could be used to gain an understanding of common software/applications running on systems within the network.

3. ***Log Enumeration***: Adversaries may enumerate system and service logs to find useful data. These logs may highlight various types of valuable insights for an adversary, such as user authentication records (Account Discovery), security or vulnerable software (Software Discovery), or hosts within a compromised network.

#### 10. Lateral Movement
The adversary is trying to move through your environment.

##### Examples
1. ***Internal Spearphishing***: After they already have access to accounts or systems within the environment, adversaries may use internal spearphishing to gain access to additional information or compromise other users within the same organization.

2. ***Lateral Tool Transfer***: Adversaries may transfer tools or other files between systems in a compromised environment. Once brought into the victim environment, files may then be copied from one system to another. Files can also be transferred using native or otherwise present tools on the victim system, such as scp, rsync, curl, sftp, and ftp.

3. ***Software Deployment Tools***: A software deployment tool is a system or application used to automate the process of distributing and installing software onto target systems or environments. Adversaries may gain access to and use centralized software suites installed within an enterprise to execute commands and move laterally through the network.

#### 11. Collection
The adversary is trying to gather data of interest to their goal.

##### Examples
1. ***Email Collection***: Adversaries may target user email to collect sensitive information. Emails may contain sensitive data, including trade secrets or personal information, that can prove valuable to adversaries.

2. ***Adversary-in-the-Middle***: This can include DHCP spoofing, ARP cache poisoning.

3. ***Screen/Input/Audio Capture***

4. ***Browser Session Hijacking***: when an adversary injects software into a browser that allows them to inherit cookies, HTTP sessions, and SSL client certificates of a user. Then, With these permissions, an adversary could potentially browse to any resource on an intranet, such as Sharepoint or webmail, that is accessible through the browser and which the browser has sufficient permissions.
   
#### 12. Command and Control
The adversary is trying to communicate with compromised systems to control them.

##### Examples
1. ***Data Encoding***: Adversaries may encode data to make the content of command and control traffic more difficult to detect.

2. ***Proxy***: Adversaries may use a connection proxy to direct network traffic between systems or act as an intermediary for network communications to a command and control server to avoid direct connections to their infrastructure. 

3. ***Remote Access Software***: An adversary may use legitimate desktop support and remote access software to establish an interactive command and control channel to target systems within networks. These services, such as VNC, Team Viewer, AnyDesk, ScreenConnect, LogMein, AmmyyAdmin, and other remote monitoring and management (RMM) tools, are commonly used as legitimate technical support software.

#### 13. Exfiltration
The adversary is trying to steal data.

##### Examples
1. ***Automated Exfiltration***: Adversaries may exfiltrate data, such as sensitive documents, through the use of automated processing after being gathered during Collection.

2. ***Exfiltration Over Alternative Protocol***: Adversaries may steal data by exfiltrating it over a different protocol than that of the existing command and control channel. Alternate protocols include FTP, SMTP, HTTP/S, DNS, SMB, or any other network protocol not being used as the main command and control channel.

3. ***Exfiltration Over Web Service***: Adversaries may use an existing, legitimate external Web service to exfiltrate data rather than their primary command and control channel. Popular Web services acting as an exfiltration mechanism may give a significant amount of cover due to the likelihood that hosts within a network are already communicating with them prior to compromise. Examples include Google Drive, Cloudflare services, etc.

#### 14. Impact
The adversary is trying to manipulate, interrupt, or destroy your systems and data.

##### Examples
1. ***Data Destruction***: Adversaries may destroy data and files on specific systems or in large numbers on a network to interrupt availability to systems, services, and network resources. D

2. ***Network Denial of Service***: Adversaries may perform Network Denial of Service (DoS) attacks to degrade or block the availability of targeted resources to users. Network DoS can be performed by exhausting the network bandwidth services rely on. Example resources include specific websites, email services, DNS, and web-based applications.

3. ***Data Manipulation***: Adversaries may insert, delete, or manipulate data in order to influence external outcomes or hide activity, thus threatening the integrity of the data.[1] By manipulating data, adversaries may attempt to affect a business process, organizational understanding, or decision making.

## CAR
The Cyber Analytics Repository (CAR) is a collection of cyber threat detection analytics. These analytics aid security professional to detect TTPs given in ATT&CK by providing the pseudocode as well as specific tools like (e.g., Splunk, EQL) 

## ENGAGE
The MITRE ENGAGE framework is a methodology designed to help organizations understand and improve their cybersecurity posture by focusing on cyber threat intelligence (CTI) analysis and threat actor engagement.

MITRE Engage is considered an Adversary Engagement Approach. This is accomplished by the implementation of Cyber Denial and Cyber Deception: 
- With Cyber Denial we prevent the adversary's ability to conduct their operations
- With Cyber Deception we intentionally plant artifacts to mislead the adversary. 

ENGAGE matrix contains the following categories:
1. Prepare the set of operational actions that will lead to your desired outcome (input)
2. Expose adversaries when they trigger your deployed deception activities 
3. Affect adversaries by performing actions that will have a negative impact on their operations
4. Elicit information by observing the adversary and learn more about their modus operandi (TTPs)
5. Understand the outcomes of the operational actions (output)

To conclde, it aid us to plan and set decoys and honeybots (like fake accounts, or isolated environment where malware can run) for the threat actors so that we can observe, prevent, and understand their methodology.

## D3FEND
D3FEND is a complementary project to ATT&CK that focuses on defensive techniques and countermeasures. It provides a structured framework for organizing and understanding defensive cybersecurity strategies, helping organizations better defend against cyber threats by mapping defensive techniques to the ATT&CK framework's offensive tactics and techniques.
