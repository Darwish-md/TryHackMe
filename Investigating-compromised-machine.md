# Windows
## Scheduled Tasks
- Task Scheduler > Task Scheduler Library

## Event Logs
- Event Viewer > Windows Logs > Application/System/Security:
  - Service Installations: 7045
  - Process Creation Events: 4688
  - Failed/Unusual Login Attempts: 4625 failed, 4624 successful
  - Driver Installation: 7034
- Get-WinEvent
  
## Running processes
- Task Manager (Ctrl + Shift + Esc) or Process Explorer from Sysinternals:
  - C:\Users\Username\AppData\ or Temp directories.
 
## Startup items
- `msconfig`
- HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run

## Installed programs
- Control Panel > Programs and Features

## Network connections
- `netstat -ano` or use TCPView (Sysinternals)

## Suspicious files
- C:\Users\[YourUser]\AppData\Local\Temp
- Check system folders like C:\Windows\, C:\Program Files\, and user directories (C:\Users\).

## Examine Browser History/Extensions

## Review User Accounts and Permissions
- Control Panel > User Accounts or `lusrmgr.msc`

## Check Windows Defender Firewall Logs
- Control Panel > System and Security > Windows Defender Firewall > Advanced Settings

## Look for Persistence Mechanisms
- Autoruns from sysinternals

# Linux
## Bash History Logs
- cat /root/.bash_history
- cat /home/username/.bash_history

## Cron logs
- grep CRON /var/log/syslog
- cat /var/log/cron

## Running processes
- `ps aux`
  - Use the lsof command to see if any processes are opening unexpected files: `lsof -p <PID>`
- top/htop: Check resource usage to see if there are any processes using unusually high CPU, memory, or I/O resources.
- Use `pstree` to see a hierarchical view of processes and check for unusual parent-child process relationships:

## Network Connections
- netstat -tuln for 
- netstat -anp for

## Suspicious Users and Groups
- cat /etc/passwd
- cat /etc/shadow
- cat /etc/sudoers

## Logins
- View the history of logins to the system.
  - last
  - lastb

## Crontabs
- crontab -l
- sudo crontab -l -u username
- for global: cat /etc/crontab







