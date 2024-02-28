### TCPView:
"TCPView is a Windows program that will show you detailed listings of all TCP and UDP endpoints on your system, including the local and remote addresses and state of TCP connections. TCPView provides a more informative and conveniently presented subset of the Netstat program that ships with Windows. The TCPView download includes Tcpvcon, a command-line version with the same functionality." 

### Process Explorer:
"The Process Explorer display consists of two sub-windows. The top window always shows a list of the currently active processes, including the names of their owning accounts, whereas the information displayed in the bottom window depends on the mode that Process Explorer is in: if it is in handle mode, you'll see the handles that the process selected in the top window has opened; if Process Explorer is in DLL mode you'll see the DLLs and memory-mapped files that the process has loaded." 

### Windows Event Logs
- The events in these log files are stored in a proprietary binary format with a .evt or .evtx extension. The raw data can be translated into XML using the Windows API. The log files with the .evtx file extension typically reside in `C:\Windows\System32\winevt\Logs`
- There are three main ways of accessing these event logs within a Windows system:
  - Event Viewer (GUI-based application)
  - Wevtutil.exe (command-line tool)
  - Get-WinEvent (PowerShell cmdlet)

### Sysmon:
- Sysmon is a tool that gathers detailed and high-quality logs as well as event tracing that assists in identifying anomalies in Windows machines. It is commonly used with a security information and event management (SIEM) system or other log parsing solutions that aggregate, filter, and visualize events. 

### OSQuery
- Osquery is an open-source tool used to query an endpoint (or multiple endpoints) using SQL syntax (Windows, Linux, macOS, and FreeBSD).
- Osquery only allows you to query events inside the machine. But with Kolide Fleet, you can query multiple endpoints from the Kolide Fleet UI instead of using Osquery locally to query an endpoint.

### Wazuh:
- Wazuh is an open-source extensive EDR solution which Security Engineers can deploy in all scales of environments.

## So what's an EDR?
- Endpoint detection and response (EDR) are tools and applications that monitor devices for an activity that could indicate a threat or security breach. These tools and applications have features that include:
  - Auditing a device for common vulnerabilities.
  - Proactively monitoring a device for suspicious activity such as unauthorized logins, brute-force attacks, or privilege escalations.
  - Visualizing complex data and events into neat and trendy graphs.
  - Recording a device's normal operating behaviour to help with detecting anomalies.

### Event Correlation:
- Event correlation deals with identifying significant artefacts co-existing from different log sources and connecting each related artefact. 

> For example, a network connection log may exist in various log sources such as Sysmon logs (Event ID 3: Network Connection) and Firewall Logs. The Firewall log may provide the source and destination IP, source and destination port, protocol, and the action taken. In contrast, Sysmon logs may give the process that invoked the network connection and the user running the process.

- Event correlation can build the puzzle pieces to complete the exact scenario from an investigation.
