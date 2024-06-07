## DFIR Digital Forensics and Incident Response
This field covers the collection of forensic artifacts from digital devices to:
- help Security Professionals identify footprints left by an attacker when a security incident occurs,
- use them to determine the extent of compromise in an environment,
- and restore the environment to the state it was before the incident occurred.

### DFIR aids security professionals in:
- Detecting Attacker Activity
- Removing Attackers
- Determining Breach Scope
- Identifying Vulnerabilities
- Understanding Attacker Behavior
- Sharing Information

### Main Concepts of DFIR
#### Artifacts:
Artifacts are pieces of evidence that point to an activity performed on a system.
> For example, if we are to claim that the attacker used Windows registry keys to maintain persistence on a system, we can use the said registry key to support our claim. In this case, the mentioned registry key will be considered an artifact.

#### Evidence Preservation:
It's crucial to maintain evidence integrity. Best practices dictate that evidence should be collected and write-protected to prevent contamination. This involves creating a secure, unalterable copy for analysis, preserving the original evidence. If the copy is corrupted during analysis, a new copy can be made from the preserved evidence.

#### Chain of Custody:
When the evidence is collected, it must be made sure that it is kept in secure custody. Any person not related to the investigation must not possess the evidence.
> For example, suppose a hard drive image, while being transferred from the person who took the image to the person who will perform the analysis, gets into the hands of a person who is not qualified to handle such evidence. In that case, we can't be sure if he dealt with the evidence correctly and hence didn't contaminate the evidence with his activity.

#### order of Volatility:
While performing DFIR, it is vital to understand the order of volatility of the different evidence sources to capture and preserve accordingly.
> For example, data in RAM will be lost when the computer is shut down, however a hard drive is persistent storage and maintains the data even if power is lost. And hence, we will need to preserve the RAM before preserving the hard drive since we might lose data in the RAM if we don't prioritize it.

#### Timeline creation:
Timeline creation provides perspective to the investigation and helps collate information from various sources to create a story of how things happened. 

### IR Methods
IR Methods were published by NIST and SANS which are almost identical. Here SANS Method (PICERL) will be discussed:
- Preparation: Before an incident happens, preparation needs to be done so that everyone is ready in case of an incident. Preparation includes having the required people, processes, and technology to prevent and respond to incidents.
- Identification: An incident is identified through some indicators in the identification phase. These indicators are then analyzed for False Positives, documented, and communicated to the relevant stakeholders.
- Containment: In this phase, the incident is contained, and efforts are made to limit its effects. There can be short-term and long-term fixes for containing the threat based on forensic analysis of the incident that will be a part of this phase.
- Eradication: Next, the threat is eradicated from the network. It has to be ensured that a proper forensic analysis is performed and the threat is effectively contained before eradication. For example, if the entry point of the threat actor into the network is not plugged, the threat will not be effectively eradicated, and the actor can gain a foothold again.
- Recovery: Once the threat is removed from the network, the services that had been disrupted are brought back as they were before the incident happened.
- Lessons Learned: Finally, a review of the incident is performed, the incident is documented, and steps are taken based on the findings from the incident to make sure that the team is better prepared for the next time an incident occurs.
