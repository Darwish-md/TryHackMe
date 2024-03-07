Event logs record events taking place in the execution of a system to provide an audit trail that can be used to understand the activity of the system and to diagnose problems. 

### Elements form event logs in Windows systems:
- System Logs: > hardware changes, device drivers, system changes, and other activities related to the device.
- Security Logs: > logon and logoff activities on a device. 
- Application Logs: > application errors, events, and warnings.
- Directory Service Events: Active Directory changes and activities are recorded in these logs, mainly on domain controllers.
- File Replication Service Events: Records events associated with Windows Servers during the sharing of Group Policies and logon scripts to domain controllers, from where they may be accessed by the users through the client servers.
- DNS Event Logs: DNS servers use these logs to record domain events and to map out
- Custom Logs: Events are logged by applications that require custom data storage. This allows applications to control the log size or attach other parameters, such as ACLs, for security purposes.

### Event logs can be classified into:
[Error, Warning, Information, Success audit, Failure audit]
### There are three main ways of accessing these event logs within a Windows system:
- Event Viewer (GUI-based application)
- `Wevtutil.exe` (command-line tool). - use /? to see the options on using the command util.
- `Get-WinEvent` (PowerShell cmdlet). - replaces the `Get-EventLog` cmdlet. 

### XPath:
XPath, XML Path Language in full, provides a standard syntax and semantics for addressing parts of an XML document and manipulating strings, numbers, and booleans. 

#### Examples of using XPath to filter events:
- `Get-WinEvent -LogName Application -FilterXPath '*/System/'`
- `Get-WinEvent -LogName Application -FilterXPath '*/EventData/'`
- `Get-WinEvent -LogName Application -FilterXPath '*/System/EventID=101 and */System/Provider[@Name="WLMS"]'`
- `Get-WinEvent -LogName Security -FilterXPath '*/EventData/Data[@Name="TargetUserName"]="System"'`

### Notes
- To count how many objects were printed by PowerShell in the terminal, we can use `| measure-object` or `(command).count`.
- A cmdlet, pronounced "command-let," is a lightweight command used to perform a specific task or operation within the PowerShell environment. Cmdlets follow a consistent naming convention of verb-noun, where the verb describes the action to be performed and the noun describes the target or object on which the action is performed.
- When working with large event logs, per Microsoft, it's inefficient to send objects down the pipeline to a Where-Object command. The use of the Get-WinEvent cmdlet's FilterHashtable parameter is recommended to filter event logs.
  > Example: This command `Get-WinEvent -LogName Application | Where-Object { $_.ProviderName -Match 'WLMS' }` can be replaced by `Get-WinEvent -FilterHashtable @{LogName='Application'; ProviderName='WLMS'}`
- We can get help for cmdlets by `Get-Help`.
- To access an evtx file in ps, we can use the -path argument like `Get-WinEvent -Path C:\Users\Administrator\Desktop\merged.evtx -FilterPath '*/System/EventID=400'`
