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
1. Spearphishing: a type of phishing attack that targets specific individuals or organizations in order to steal personal information that can lead to have access to an account, help attackers in the later procedures, etc

2. Search open websites/domains : Adversaries may search freely available websites and/or domains for information about victims that can be used during targeting. Information about victims may be available in various online sites, such as social media, new sites. it contains 3 sub-techniques which are [social media, search engines (google dorks for example), code repositories].

3. Adversaries may search and gather information about victims from closed sources
#### 2. Resource Development
The adversary is trying to establish resources they can use to support operations.

##### Examples

#### 3. Initial Access	
The adversary is trying to get into your network.

##### Examples

#### 4. Execution	
The adversary is trying to run malicious code.

##### Examples

#### 5. Persistence	
The adversary is trying to maintain their foothold.

##### Examples

#### 6. Privilege Escalation
The adversary is trying to gain higher-level permissions.

##### Examples

#### 7. Defense Evasion
The adversary is trying to avoid being detected.

##### Examples

#### 8. Credential Access
The adversary is trying to steal account names and passwords.

##### Examples

#### 9. Discovery
The adversary is trying to figure out your environment.

##### Examples

#### 10. Lateral Movement
The adversary is trying to move through your environment.

##### Examples

#### 11. Collection
The adversary is trying to gather data of interest to their goal.

##### Examples

#### 12. Command and Control
The adversary is trying to communicate with compromised systems to control them.

##### Examples

#### 13. Exfiltration
The adversary is trying to steal data.

##### Examples

#### 14. Impact
The adversary is trying to manipulate, interrupt, or destroy your systems and data.

##### Examples


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
