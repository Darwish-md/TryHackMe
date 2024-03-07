#### Sysmon is a sysinternal tool used to monitor and log events to the Windows Event Logs based on the rules set in the configuration file. these rules are either excluding or including specific conditions and whenever a rule is triggered, an alert is being raised and sent to SIEM or the responsible monitoring agent.

#### Events within Sysmon are stored in Applications and Services `Logs/Microsoft/Windows/Sysmon/Operational`.

#### Sysmon requires a config file in order to tell the binary how to analyze the events that it is receiving. Sysmon includes 29 different types of Event IDs like Process Creation, CreateRemoteThread, etc.

#### To start Sysmon, this command is used `Sysmon.exe -accepteula -i <File_PATH>`.


