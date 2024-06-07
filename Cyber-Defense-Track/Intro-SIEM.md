## SIEM
- It is a tool that ***collects*** data from various endpoints/network devices across the network, ***stores*** them at a centralized place, and ***performs*** correlation on them. 

### There are 2 types of log sources:
1. Host-Centric Log Sources
These are log sources that capture events that occurred within or related to the host. Some log sources that generate host-centric logs are Windows Event logs, Sysmon, Osquery, etc.

2. Network-Centric Log Sources
Network-related logs are generated when the hosts communicate with each other or access the internet to visit a website. Some network-based protocols are SSH, VPN, HTTP/s, FTP, etc.

### Common devices that are found in a network environment:
1. Windows machine: To view events in a Windows environment, type Event Viewer in the search bar, and it takes you to the tool where different logs are stored and can be viewed.
2. Linux machine:
Some of the common locations where Linux store logs are:
- `/var/log/httpd` : Contains HTTP Request  / Response and error logs.
- `/var/log/cron`   : Events related to cron jobs are stored in this location.
- `/var/log/auth.log and /var/log/secure` : Stores authentication related logs.
- `/var/log/kern` : This file stores kernel related events.
3. Web server:
In Linux, common locations to write all apache related logs are `/var/log/apache` or `/var/log/httpd`.

### Log ingestion:
Each SIEM solution has its own way of ingesting the logs. Some common methods used by SIEM solutions:

1) Agent / Forwarder: These SIEM solutions provide a lightweight tool called an agent (forwarder by Splunk) that gets installed in the Endpoint. It is configured to capture all the important logs and send them to the SIEM server.
2) Syslog: Syslog is a widely used protocol to collect data from various systems like web servers, databases, etc., are sent real-time data to the centralized destination.
3) Manual Upload: Some SIEM solutions, like Splunk, ELK, etc., allow users to ingest offline data for quick analysis. Once the data is ingested, it is normalized and made available for analysis.
4) Port-Forwarding: SIEM solutions can also be configured to listen on a certain port, and then the endpoints forward the data to the SIEM instance on the listening port.
