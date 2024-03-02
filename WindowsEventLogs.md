Event logs record events taking place in the execution of a system to provide an audit trail that can be used to understand the activity of the system and to diagnose problems. 

#### Elements form event logs in Windows systems:
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
#### Event Viewer (GUI-based application)
#### Wevtutil.exe (command-line tool)
#### Get-WinEvent (PowerShell cmdlet)
  
