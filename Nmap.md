# Nmap host scan
### Examples of target specification are:
- list: MACHINE_IP scanme.nmap.org example.com will scan 3 IP addresses.
- range: 10.11.12.15-20 will scan 6 IP addresses: 10.11.12.15, 10.11.12.16,… and 10.11.12.20.
- subnet: MACHINE_IP/30 will scan 4 IP addresses.
- File as input: nmap `-iL list_of_hosts.txt`

### Nmap follows the following approaches to discover live hosts
- When a privileged user tries to scan targets on a local network (Ethernet), Nmap uses ARP requests. A privileged user is root or a user who belongs to sudoers and can run sudo.
- When a privileged user tries to scan targets outside the local network, Nmap uses ICMP echo requests, TCP ACK (Acknowledge) to port 80, TCP SYN (Synchronize) to port 443, and ICMP timestamp request.
- When an unprivileged user tries to scan targets outside the local network, Nmap resorts to a TCP 3-way handshake by sending SYN packets to ports 80 and 443.

## NMAP target calculation
Suppose we sending `10.10.12.13/29` as a target for the scan, then to find out the list of targets:
1. The subnet mask would be 29 bits and only 3 bits for the subnetwork. For the given address, the 13 is represented as `00001101`.
2. Find the network address:
  - Applying the bitwise operation: `00001010.00001010.00001100.00001101` AND `11111111.11111111.11111111.11111000` which results to `00001010.00001010.00001100.00001000` (which is 10.10.12.8).
3. The number of IPs in this subnetwork is 2ˆ(32-29)=2ˆ3=8, however 10.10.12.8 is the network address and 10.10.12.15 is the broadcast IP which leaves us with 6 total number of usable IPs for hosts.

## Notes
- If you don’t want Nmap to the DNS server, you can add `-n`.
- `nmap -sL TARGETS` to list the targets nmap will scan, while to show how many Run `nmap -sL -n TARGETS`.
- If you want to use Nmap to discover online hosts without port-scanning the live systems, you can issue `nmap -sn TARGETS`.
  
- To scan using ARP requests: `nmap -PR TARGETS`, and without port scanning: `nmap -PR -sn TARGETS`.
- To use ICMP echo request to discover live hosts, add the option `-PE`.
- Adding the `-PP` option tells Nmap to use ICMP timestamp requests.
- Nmap uses address mask queries (ICMP Type 17) and checks whether it gets an address mask reply (ICMP Type 18). This scan can be enabled with the option `-PM`.
- To use TCP SYN ping, you can do so via the option `-PS` followed by the port number, range, list, or a combination of them. For example, `-PS21` will target port 21, while `-PS21-25` will target ports 21, 22, 23, 24, and 25. Finally `-PS80,443,8080` will target the three ports 80, 443, and 8080.
- To send a packet with an ACK flag set: `-PA`
-  Nmap uses `-PU` for UDP ping.

-  Nmap look up for online hosts; however, we can use the option `-R` to query the DNS server even for offline hosts. If you want to use a specific DNS server, we can add the `--dns-servers DNS_SERVER option`.
- `-P` is used primarily for host discovery (ping scan), while `-s` is used for port scanning to determine the state of each port (open, closed, or filtered) on the target host.
- `-v` can be used to show the results as the scan progresses.

# Nmap port scan

## States of ports

Nmap considers the following six states:
- Open: indicates that a service is listening on the specified port.
- Closed: indicates that no service is listening on the specified port, although the port is accessible. By accessible, we mean that it is reachable and is not blocked by a firewall or other security appliances/programs.
- Filtered: means that Nmap cannot determine if the port is open or closed because the port is not accessible. This state is usually due to a firewall preventing Nmap from reaching that port. Nmap’s packets may be blocked from reaching the port; alternatively, the responses are blocked from reaching Nmap’s host.
- Unfiltered: means that Nmap cannot determine if the port is open or closed, although the port is accessible. This state is encountered when using an ACK scan -sA.
- Open|Filtered: This means that Nmap cannot determine whether the port is open or filtered.
- Closed|Filtered: This means that Nmap cannot decide whether a port is closed or filtered.

## TCP header flags

1. URG: Urgent flag indicates that the urgent pointer filed is significant. The urgent pointer indicates that the incoming data is urgent, and that a TCP segment with the URG flag set is processed immediately without consideration of having to wait on previously sent TCP segments.
2. ACK: Acknowledgement flag indicates that the acknowledgement number is significant. It is used to acknowledge the receipt of a TCP segment.
3. PSH: Push flag asking TCP to pass the data to the application promptly.
4. RST: Reset flag is used to reset the connection. Another device, such as a firewall, might send it to tear a TCP connection. This flag is also used when data is sent to a host and there is no service on the receiving end to answer.
5. SYN: Synchronize flag is used to initiate a TCP 3-way handshake and synchronize sequence numbers with the other host. The sequence number should be set randomly during TCP connection establishment.
6. FIN: The sender has no more data to send.

## Port Scanning Types

#### TCP Connect Scan
TCP connect scan works by completing the TCP 3-way handshake:
1. SYN
2. SYN/ACK
3. ACK
4. RST/ACK

To run the scan: `nmap -sT TARGET`.

- we can use `-F` to enable fast mode and decrease the number of scanned ports from 1000 to 100 most common ports. 
- the `-r` option can also be added to scan the ports in consecutive order instead of random order.
- Unprivileged users are limited to connect scan.
  
#### TCP SYN Scan
The default scan mode for Nmap is SYN scan, and it requires a privileged (root or sudoer). We can select this scan type by using the `-sS` option.

It works like in the following:
1. SYN
2. SYN/ACK
3. RST

Because we didn’t establish a TCP connection, this decreases the chances of the scan being logged.

#### UDP Scan
When Scanning udp ports, we have 3 states:
- Either we receive a response as for example: Nmap sends a UDP packet to port 53 (DNS), and receives a DNS response. In this case the port will be stated as indeed open.
- We don't receive any response, and in this case the port will be stated as open|filtered. This ambiguity arises because the lack of response could mean that the port is open but no application is actively responding to the probe, or the port is filtered by a firewall and the packets are being silently dropped.
- The third possibility is when the port is closed and hence we receive back ICMP Type 3 "Destination Unreachable".

We can run the scan by `-sU`.

## Fine-tuning scope & Performance  
You can specify the ports you want to scan instead of the default 1000 ports:
- port list: `-p22,80,443` will scan ports 22, 80 and 443.
- port range: `-p1-1023 will scan all ports between 1 and 1023 inclusive.
- You can request the scan of all ports by using -p-, which will scan all 65535 ports. 
- You can control the scan timing using -T<0-5> where:
  - paranoid (0)
  - sneaky (1)
  - polite (2)
  - normal (3)
  - aggressive (4)
  - insane (5)
- you can choose to control the packet rate using `--min-rate <number>` and `--max-rate <number>
- you can control probing parallelization using `--min-parallelism <numprobes>` and `--max-parallelism <numprobes>`
