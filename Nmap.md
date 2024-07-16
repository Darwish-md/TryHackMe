
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
