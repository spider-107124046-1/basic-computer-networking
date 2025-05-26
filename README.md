# Computer Networking

***

## Analysis Questions

**1. What types of traffic are present?**

![image](https://github.com/user-attachments/assets/56791775-e9ca-4a18-b045-dcff3a08e7d5)

- Hypertext Transfer Protocol (HTTP, over TCP)
- Domain Name System (DNS, over UDP)
- Multicast Domain Name System (mDNS, over UDP)
- TCP Handshakes

**2. How many DNS queries were made in total?**

`dns.flags.response == 0` yields 358 results, one of which is an mDNS query.
357 DNS queries + 1 mDNS query = **358** queries

**3. What types of DNS queries were made?**

- A (hostname -> IPv4 Address)
- AAAA (hostname -> IPv6 Address)
- HTTPS (service binding)
- PTR (IPv4 Address -> allowed hostnames)

**4. What is a Loopback Interface?**

- **Interface?** A network interface is the point of interconnection between the device and the network. Network interfaces can be **physical** (hardware based, like Ethernet NIC cards and Wi-Fi adapters), or **virtual** (software, created for purposes such as internally isolating networks)

![image](https://github.com/user-attachments/assets/8d31f456-9887-4091-a1e0-c074b1feb26a)

- **Loopback?** Loopback interface is a virtual interface created by the OS's networking stack, on the subnet 127.0.0.0/8. Any communications with this interface is routed to the device itself. The most common address for referring to the device itself on the loopback interface is 127.0.0.1. `systemd-resolved`, a service in Linux-based operating systems that use `systemd` as their init daemon (basically, a system manager), that provides network name resolution to local applications, has address `127.0.0.53`. DNS queries of applications are routed to 127.0.0.53, which are then resolved by systemd-resolved (by forwarding the DNS query to the *actual* DNS server configured for usage in the network).

**5. How many .txt files were requested? List their names.**

![image](https://github.com/user-attachments/assets/c6e7cb32-364a-428b-b6fb-7fe86af4df1c)

**Three. `decoy2.txt`, `encoded.txt`, `decoy1.txt`**

