
### Examples of target specification are:
- list: MACHINE_IP scanme.nmap.org example.com will scan 3 IP addresses.
- range: 10.11.12.15-20 will scan 6 IP addresses: 10.11.12.15, 10.11.12.16,… and 10.11.12.20.
- subnet: MACHINE_IP/30 will scan 4 IP addresses.
- File as input: nmap ´-iL list_of_hosts.txt´.


## Notes
- If you don’t want Nmap to the DNS server, you can add ´-n´.
