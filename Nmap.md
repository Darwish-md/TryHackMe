# Nmap Host Scan
### Examples of target specification are:
- list: MACHINE_IP scanme.nmap.org example.com will scan 3 IP addresses.
- range: 10.11.12.15-20 will scan 6 IP addresses: 10.11.12.15, 10.11.12.16,… and 10.11.12.20.
- subnet: MACHINE_IP/30 will scan 4 IP addresses.
- File as input: nmap `-iL list_of_hosts.txt`

### Nmap follows the following approaches to discover live hosts
- When a privileged user tries to scan targets on a local network (Ethernet), Nmap uses ARP requests. A privileged user is root or a user who belongs to sudoers and can run sudo.
- When a privileged user tries to scan targets outside the local network, Nmap uses ICMP echo requests, TCP ACK (Acknowledge) to port 80, TCP SYN (Synchronize) to port 443, and ICMP timestamp request.
- When an unprivileged user tries to scan targets outside the local network, Nmap resorts to a TCP 3-way handshake by sending SYN packets to ports 80 and 443.

### NMAP target calculation
Suppose we sending `10.10.12.13/29` as a target for the scan, then to find out the list of targets:
1. The subnet mask would be 29 bits and only 3 bits for the subnetwork. For the given address, the 13 is represented as `00001101`.
2. Find the network address:
  - Applying the bitwise operation: `00001010.00001010.00001100.00001101` AND `11111111.11111111.11111111.11111000` which results to `00001010.00001010.00001100.00001000` (which is 10.10.12.8).
3. The number of IPs in this subnetwork is 2ˆ(32-29)=2ˆ3=8, however 10.10.12.8 is the network address and 10.10.12.15 is the broadcast IP which leaves us with 6 total number of usable IPs for hosts.


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

### Basic Scans
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

## Advanced Scans

#### Null Scan
A TCP packet with no flags set will not trigger any response when it reaches an open port. so in null scan, we have two states:
1. We receive no reply back, which means the port is open or filtered due to firewall rules.
2. We receive a RST/ACK and would indicate the port is closed.

A null scan can be run with the flag `-sN`.

#### FIN Scan
Same to Null scan. It's worth noting some firewalls will 'silently' drop the traffic without sending an RST.

It can be run with the flag `-sF`.

#### Xmas Scan
An Xmas scan sets the FIN, PSH, and URG flags simultaneously. You can select Xmas scan with the option `-sX`.

Like the Null scan and FIN scan, if an RST packet is received, it means that the port is closed. Otherwise, it will be reported as open|filtered.

Using a flag combination that does not match the SYN packet makes it possible to deceive the firewall and reach the system behind it. However, a stateful firewall will practically block all such crafted packets and render this kind of scan useless.

#### Maimos Scan
In this scan, the FIN and ACK bits are set. The target should send an RST packet as a response. However, certain BSD-derived systems drop the packet if it is an open port exposing the open ports. To select this scan type, use the `-sM`.

Most target systems respond with an RST packet regardless of whether the TCP port is open. In such a case, we won’t be able to discover the open ports. 

#### Ack Scan
When sending an Ack packet, the target would respond to the ACK with RST regardless of the state of the port. Hence, this kind of scan would be helpful if there is a firewall in front of the target. 

Consequently, based on which ACK packets resulted in responses, you will learn which ports were not blocked by the firewall. In other words, this type of scan is more suitable to discover firewall rule sets and configuration.

There is one state in this scan, unfiltered which indicates the ports are open. 

Use the `-sA` option to choose this scan.

#### Window Scan
The TCP window scan is almost the same as the ACK scan; however, it examines the TCP Window field of the RST packets returned. we expect to get an RST packet in reply to our “uninvited” ACK packets, regardless of whether the port is open or closed.

Similar to Ack scan, it is helpful if there is a firewall set up for the target. it returns `closed` for the ports which are not blocked by firewall.

You can select this scan type with the option `-sW`.

#### Custom Scan
If you want to experiment with a new TCP flag combination beyond the built-in TCP scan types, you can do so using `--scanflags`. For instance, if you want to set SYN, RST, and FIN simultaneously, you can do so using `--scanflags RSTSYNFIN`.

#### Idle/Zombie Scan
The idle (zombie) scan requires the following three steps to discover whether a port is open:
1. Trigger the idle host to respond so that you can record the current IP ID on the idle host.
2. Send a SYN packet to a TCP port on the target. The packet should be spoofed to appear as if it was coming from the idle host (zombie) IP address. Three scenarios would arise:
   - In the first scenario, the TCP port is closed; therefore, the target machine responds to the idle host with an RST packet. The idle host does not respond; hence its IP ID is not incremented.
   - In the second scenario, the TCP port is open, so the target machine responds with a SYN/ACK to the idle host (zombie). The idle host responds to this unexpected packet with an RST packet, thus incrementing its IP ID.
   - In the third scenario, the target machine does not respond at all due to firewall rules. This lack of response will lead to the same result as with the closed port; the idle host won’t increase the IP ID.
3. Trigger the idle machine again to respond so that you can compare the new IP ID with the one received earlier. If the difference is 1, it means the port on the target machine was closed or filtered. However, if the difference is 2, it means that the port on the target was open.

## Spoofing & Decoys
If we launch `nmap -S SPOOFED_IP 10.10.16.28`, Nmap will craft all the packets using the provided source IP address `SPOOFED_IP`. The target machine will respond to the incoming packets sending the replies to the destination IP address SPOOFED_IP. For this scan to work and give accurate results, the attacker needs to monitor the network traffic to analyze the replies.

we can issue `nmap -e NET_INTERFACE -Pn -S SPOOFED_IP 10.10.16.28` to tell Nmap explicitly which network interface to use and not to expect to receive a ping reply. 

if the attacker and the target machine are on the same Ethernet (802.3) network or same WiFi (802.11), they can spoof the madc address as well with `--spoof-mac SPOOFED_MAC`.

The concept of decoys is simple, make the scan appear to be coming from many IP addresses so that the attacker’s IP address would be lost among them.

`nmap -D 10.10.0.1,10.10.0.2,RND,RND,ME 10.10.16.28` will make the scan of 10.10.16.28 appear as coming from the IP addresses 10.10.0.1, 10.10.0.2, two random IPs, and then attacker's IP.

## Fragmentation
Nmap provides the option `-f` to fragment packets. Once chosen, the IP data will be divided into 8 bytes or less. Adding another -f (`-f -f` or `-ff`) will split the data into 16 byte-fragments instead of 8. You can change the default value by using the `--mtu`; however, you should always choose a multiple of 8.

If the TCP segment has a size of 64, and -ff option is being used, how many IP fragments will you get? The answer would be 64/16 = 4 fragments

On the other hand, if you prefer to increase the size of your packets to make them look innocuous, you can use the option `--data-length NUM`, where num specifies the number of bytes you want to append to your packets.

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

# Post Port Scans
#### Service Detection
Adding -sV to your Nmap command will collect and determine service and version information for the open ports.

You can control the intensity with `--version-intensity LEVEL` where the level ranges between 0, the lightest, and 9, the most complete. `-sV --version-light` has an intensity of 2, while `-sV --version-all` has an intensity of 9.

It is important to note that using -sV will force Nmap to proceed with the TCP 3-way handshake and establish the connection to recognize the service. In other words, stealth SYN scan -sS is not possible when -sV option is chosen.

#### OS Detection
OS detection can be enabled using `-O` like `nmap -sS -O 10.10.255.4`. 

The OS detection is very convenient, but many factors might affect its accuracy. First and foremost, Nmap needs to find at least one open and one closed port on the target to make a reliable guess. Furthermore, the guest OS fingerprints might get distorted due to the rising use of virtualization and similar technologies. 

We can use `--traceroute` to find the number of hops until the target. Ex: `nmap -sS --traceroute 10.10.255.4`. Standard traceroute starts with a packet of low TTL (Time to Live) and keeps increasing until it reaches the target. Nmap’s traceroute starts with a packet of high TTL and keeps decreasing it. It is worth mentioning that many routers are configured not to send ICMP Time-to-Live exceeded, which would prevent us from discovering their IP addresses.

#### NSE 

You can choose to run the scripts in the default category using `--script=default` or simply adding `-sC`. In addition to default, categories include auth, broadcast, brute, default, discovery, dos, exploit, external, fuzzer, intrusive, malware, safe, version, and vuln.

EX: The command `sudo nmap -sS -sC 10.10.224.147`, where -sC will ensure that Nmap will execute the default scripts following the SYN scan. 

You can also specify the script by name using `--script "SCRIPT-NAME".


# Notes
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
- In ACK and Window scans, it is vital to remember that just because a firewall is not blocking a specific port, it does not necessarily mean that a service is listening on that port. For example, there is a possibility that the firewall rules need to be updated to reflect recent service changes. Hence, ACK and window scans are exposing the firewall rules, not the services.
- Providing the `--reason` flag gives us the explicit reason why Nmap concluded that the system is up or a particular port is open.
- use `-v` for verbose output or `-vv` for even more verbosity.
- you can use `-d` for debugging details or `-dd` for even more details.
- The `-F` option instructs Nmap to scan only the top 100 most common ports. 
- the `-n` option is used to disable DNS resolution.
