#### Sysmon is a sysinternal tool used to monitor and log events to the Windows Event Logs based on the rules set in the configuration file. these rules are either excluding or including specific conditions and whenever a rule is triggered, an alert is being raised and sent to SIEM or the responsible monitoring agent.

- Events within Sysmon are stored in Applications and Services `Logs/Microsoft/Windows/Sysmon/Operational`.

- Sysmon requires a config file in order to tell the binary how to analyze the events that it is receiving. Sysmon includes 29 different types of Event IDs like Process Creation, CreateRemoteThread, etc.

- To start Sysmon, this command is used `Sysmon.exe -accepteula -i <File_PATH>`.

### Sysmon Best Practices:
- Exclude > Include
- Know your environment before implementation
- CLI gives you further control

### Examples
#### Hunting Metasploit
- Hunting for Metasploit using Event ID 3:
```
<RuleGroup name="" groupRelation="or">
	<NetworkConnect onmatch="include">
		<DestinationPort condition="is">4444</DestinationPort>
		<DestinationPort condition="is">5555</DestinationPort>
	</NetworkConnect>
</RuleGroup>
```

- And events can be queried using the filter:
```
get-WinEvent -Path C:\Users\THM-Analyst\Desktop\Scenarios\Practice\Hunting_Metasploit.evtx -FilterXPath "*/System/EventID=3 and */EventData/Data[@Name='DestinationPort']=4444"
```

#### Hunting Mimikatz
- Could be detcted by looking for files with the name in case it bypassed AV:
```
<RuleGroup name="" groupRelation="or">
	<FileCreate onmatch="include">
		<TargetFileName condition="contains">mimikatz</TargetFileName>
	</FileCreate>
</RuleGroup>
```
However, we usually check the advanced techniques like detecting abnormal LSASS behaviour. If LSASS is accessed by a process other than svchost.exe it should be considered suspicious behavior and should be investigated further, so we can trigger an alert whenever any other process is accessing lsass:
```
<RuleGroup name="" groupRelation="or">
	<ProcessAccess onmatch="exclude">
		<SourceImage condition="image">svchost.exe</SourceImage>
	</ProcessAccess>
	<ProcessAccess onmatch="include">
		<TargetImage condition="image">lsass.exe</TargetImage>
	</ProcessAccess>
</RuleGroup>
```
- And events can be queried using the filter:
```
Get-WinEvent -Path Desktop\Scenarios\Practice\Hunting_Mimikatz.evtx -FilterXPath "*/System/EventID=10 and */EventData/Data[@Name='TargetImage']='C:\Windows\system32\lsass.exe'" | Format-List *
```

