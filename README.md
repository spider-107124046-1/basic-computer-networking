# Computer Networking

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

**6. One .txt file contains base64-encoded content. Identify and decode it. What does it contain?**

![image](https://github.com/user-attachments/assets/22261c04-a01f-47ae-a15f-0207196cd694)

Contents of `encoded.txt`: `RkxBR3tzcGlkM3JfbmV0d29ya19tYXN0ZXJ9Cg==`

Decodes to: `FLAG{spid3r_network_master}`

**7. Was any attempt made to distract the analyst using decoy files? Explain.**

Yes, using two other text files (`decoy1.txt`, `decoy2.txt`) to attempt to mask the encoded text file (`encoded.txt`) being requested. *It was not effective.*

**8. Are there any known ports being used for uncommon services?**

- **Known ports?** Well-known ports are ports reserved in the range 0-1023 by the Internet Assigned Numbers Authority (IANA) for well-known (common and widely used) network services. Some most notable well-known ports:
    * SSH - **22**
    * DNS - **53**
    * HTTP - **80**
    * HTTPS (SSL/TLS) - **443**

`tcp.port <= 1024 || udp.port <= 1024` yields only DNS queries and responses, so no well-known ports are being used for uncommon services. However, the HTTP `Server: SimpleHTTP/0.6 Python/3.12.3` is running on port 8000, instead of the well-known port 80.

**9. How many HTTP GET requests are visible in the capture?**

Three.

**10. What User-Agent was used to make the HTTP requests?**

![image](https://github.com/user-attachments/assets/67d9b3d7-bf51-4a38-b4b0-282942b7265b)

`curl/8.5.0`

***

## Time Pass: Recreating the setup

Server:

[![asciicast](https://asciinema.org/a/tUkHw6z3yBlRxOeVYSSJWUKKA.svg)](https://asciinema.org/a/tUkHw6z3yBlRxOeVYSSJWUKKA)

Client:

[![asciicast](https://asciinema.org/a/36XGUSjU4PhmyTm9p8ISsubsa.svg)](https://asciinema.org/a/36XGUSjU4PhmyTm9p8ISsubsa)

Server Log:

![image](https://github.com/user-attachments/assets/885d3322-552b-41c0-9227-01d12a413739)
