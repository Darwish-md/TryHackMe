### What is YARA?
YARA (Yet Another Recursive Acronym) is a tool primarily used in malware research and detection. It provides a rule-based approach to create descriptions of malware families based on regular expression, textual or binary patterns. But not only that, it can be used by pentesters for example to search for any usernames, passwords, etc. you get the idea!

In a yara file, we have rule name, strings, and conditions to check for:
```
rule helloworld_checker{
	strings:
		$hello_world = "Hello World!"

	condition:
		$hello_world
}
```
Let's say this file is myrule.yar, then  if we wanted to use "myrule.yar" on directory "some directory", we would use the following command:`yara myrule.yar somedirectory`.

Information security researcher "fr0gger_" has recently created a handy cheatsheet that breaks down and visualises the elements of a YARA rule: `https://blog.securitybreak.io/security-infographics-9c4d3bd891ef#52a8`

### YARA Modules
Frameworks such as the ***Cuckoo Sandbox*** or ***Python's PE*** Module allow you to improve the technicality of your Yara rules ten-fold.
- Python's PE module allows you to create Yara rules from the various sections and elements of the Windows Portable Executable (PE) structure.
- Cuckoo Sandbox is an automated malware analysis environment. This module allows you to generate Yara rules based upon the behaviours discovered from Cuckoo Sandbox. As this environment executes malware, you can create rules on specific behaviours such as runtime strings and the like.

### YARA Tools
Knowing how to create custom Yara rules is useful, but luckily you don't have to create many rules from scratch to begin using Yara to search for evil. There are plenty of GitHub [resources](https://github.com/InQuest/awesome-yara?tab=readme-ov-file#rules) and open-source tools (along with commercial products) that can be utilized to leverage Yara in hunt operations and/or incident response engagements.

Examples:
- [LOKI](https://github.com/Neo23x0/Loki)
- [THOR](https://www.nextron-systems.com/thor-lite/)
- [FENRIR](https://github.com/Neo23x0/Fenrir)
- YAYA

### Creating Yara rules
yarGen or yarAnalyzer can be used to generate YARA rules. We can use this command for example: `python3 yarGen.py -m /home/cmnatic/suspicious-files/file2 --excludegood -o /home/cmnatic/suspicious-files/file2.yar`.

A brief explanation of the parameters above:
- -m is the path to the files you want to generate rules for
- --excludegood force to exclude all goodware strings (these are strings found in legitimate software and can increase false positives)
- -o location & name you want to output the Yara rule

After the new rule is created (in the mentioned example, it is file2.yar), we copy the file to the signature-base/yara directory of Loki. Now we have the new rule and can be used with Loki.

### Valhalla 
Valhalla is a database of yara rules where we can conduct searches based on a keyword, tag, ATT&CK technique, sha256, or rule name. 

Check it out [here](https://valhalla.nextron-systems.com/)
