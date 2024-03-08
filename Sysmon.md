#### Sysmon is a sysinternal tool used to monitor and log events to the Windows Event Logs based on the rules set in the configuration file. these rules are either excluding or including specific conditions and whenever a rule is triggered, an alert is being raised and sent to SIEM or the responsible monitoring agent.

- Events within Sysmon are stored in Applications and Services `Logs/Microsoft/Windows/Sysmon/Operational`.

- Sysmon requires a config file in order to tell the binary how to analyze the events that it is receiving. Sysmon includes 29 different types of Event IDs like Process Creation, CreateRemoteThread, etc.

- To start Sysmon, this command is used `Sysmon.exe -accepteula -i <File_PATH>`.

#### Sysmon Best Practices:
- Exclude > Include
- Know your environment before implementation
- CLI gives you further control

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

- And events can be found using the filter:
```
get-WinEvent -Path C:\Users\THM-Analyst\Desktop\Scenarios\Practice\Hunting_Metasploit.evtx -FilterXPath "*/System/EventID=3 and */EventData/Data[@Name='DestinationPort']=4444"
```



