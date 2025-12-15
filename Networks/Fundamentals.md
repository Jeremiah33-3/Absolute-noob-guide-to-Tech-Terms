## Links

1. Interview [questions](https://www.geeksforgeeks.org/category/computer-networks/)
2. OSI model [explanation](https://www.geeksforgeeks.dev/learn/SystemDesign/osi-model)
3. GeeksforGeeks [tutorial](https://www.geeksforgeeks.org/computer-networks/computer-network-tutorials/)
4. GeeksforGeeka [cheatsheet](https://www.geeksforgeeks.org/computer-networks/computer-network-cheat-sheet/)
5. GeeksforGeeks [interview corner](https://www.geeksforgeeks.org/interview-prep/interview-corner/)

## Broad Concepts

### VPN: Virtual Private Network
Encrpypted connection between a device and a remote server, used to protect data or access restricted content.
- How: route network traffic through a secure server
- Result: mask real IP address, making the device to appear to be from another location

### NAT: network address translation
Used to modify source or destination IP addresses of packets as they pass through a router
- Result: allows multiple devices within a local network to share a single public IP address

### VLAN
Allows network admin to create logically separated networks within a physical network, even though devices may be physically on the same network
- How: isolate traffic between physical devices for better security performance and manageability

### Routers
A device that connects different networks such as a local network to the internet
- How: use IP addresses to determine the best route for data to travel from one network to another
- provide additional features like firewalls, NAT and DHCP services

### Switches
Device that connects multiple devices within the same network
- How: use MAC, media access control, addresses to forward data to the correct device

### Firewall
A secuirty device or software that monitors and controls incoming and outcoming traffic
- How: act as a barrier between internal network and the external world by blocking unwatned traffic and allowing traffic from predefined security rules (protocols)

### OSI: Open Systems Interconnection
Conceptual model/framework that divides network communication into 7 layers
- 🧱Physical layer: deals with physical transmission of data over media like cables or wireless signals; 7 topologies (arrangement)
- 👨‍💻Data link layer: ensures reliable communication between 2 devices by managing MAC addresses and data frames
- 🥅Network layers: routes data to correct destination based on IP addresses
- 🚌Transport layer: ensures reliable end-to-end communication, providing flow control and error correction
- 🤝Session layer: manages sessions and maintains the state of communication
- 📺Presentation layer: formats and encrypts data for the application layer, ensuring data is readable
- 📱Application layer: interacts with software applications to provide network services

### WAN: Wide Area Network
A network that spans a large geographic area
- connects multiple LAN (Local area networks) togther
- Internet is the largest example of a WAN
- typically slower and more expensive to maintain than LANs, but is essential to connect devices over long distances

### LAN: local area network
A network confined to a small geographic area
- connects devices like computers, printers and servers, allowing them to share resourcs and communicate efficiently
- can be wired using ethernet cables or wireless using wi-fi
- **load balancers** distribute network traffic across multiple servers, ensuring no single server is overwhelmed with too much traffic

### MAC address
Unique identifier assigned to each network interface card, NIC
- used to connect devices to a network and helps ensure data is delivered to the correct device in a LAN
- a 48-bit address used by switches and routers to direct traffic within a local network
- operates at data link layer of OSI model

### ARP: Address Resolution Protocol
Rule sthat map an IP address to its corresponding MAC address within a local network 
- How: when a device wants to communicate with another device on the same network, it sends an ARP request to find out the recipient's MAC address (ensures data reaches the right physical device)

### ICMP: Internet Control Message Protocol
Network layer protocol used primarily for error handling and diagnostic purposes in network communications.
- `/ping` command

### VOIP: Voice over Internet Protocol
Method that converts your voice into digital data packets, which are transmitted via broadband connections. 
- unlike traditional phone systems that rely on circuit-switched networks

### NFC: Near Field Communication
Tech that allows devices to exchange data over short distances (4cm or less)
- Use cases: contactless payments, quick device pairing, and access control systems

### MPLS: Multiprotocol Label Switching
A routing technique to improve speed and latency in large traffic
- uses labels to make routing decisions, instead of solely relying on IP addresses

### SD-WAN: software-defined WAN
A modern approach to managing a wide area network
- How: uses software to control the flow of data across multiple network connections such as broadband, LTE, or MPLS

### Proxy 
A server that acts as an intermediary between a device and the internet.
- connect website through a proxy, requests are sent through the proxy server, which fetches the data and returns to you
- increase privacy, filter content, cache frequently.
- can also mask IP addresses

### QoS: quality of service
Set of traffic management techniques that ensure predictable and reliable performance or specific applications, sessions, or traffic types in a network

## Protocols

> Set of rules that dictate how devices communicate, how data moves (transit, receive), and how secure the networks are.

***
**Webs**

### HTTP: Hypertext Transfer Protocol
Primarily loads web pages, data transfer on the web (browsers <-> servers).

❗**Key shortfall**: HTTP transmits data in plain text, making it vulnerable to to interception and attacks like man-in-the-middle.

### HTTPS
HTTP but make it secured -- HTTPS encrypts data using SSL (Secure Sockets Layer) and TLS (Transport Layer Security).
- SSL and TLS are cryptographic protocols that secure communication over the internet by encrypting data and authenticating connections between clients and servers.
- TLS is the modern successor to SSL (offering stronger security)

### TCP: Transmission Control Protocol
Reliable data transmission, connection-oriented.
- ensure data packets are sent, received in the correct order and error checked for integrity.
- works tgt with IP

### IP
Routing data packets across networks.
- determines the best possible route for data packets to travel across networks.
- works tgt with TCP

### DNS: Domain Name System
- internet's phone book
- translate human friendly website names to numrical IP addresses that computers understand such as 142.250.185.206
- ❗attacks can happen: DNS spoofing where hackers manipulate domain records to redirect users to fraudulent websites, often used in phishing schemes.

### DHCP: Dynamic Host Configuration Protocol
Managing IP addresses dynamically in large networks
- automates assignment of IP addresses (instead of manual configuration by reconfiguring network settings)

***
**Cybersecurity & Hacking Protocols**

### SSH: 
secure (encrypted) remote system access.
- protect login credentials and transmitted data from eavesdroppers
- ❗Hackers can exploit misconfigured SSH services to gain unauthorised access (SSH credentials)
- Telnet, the unsecure remote login, is outdated

### SMB: Server Message Block
File and printer sharing on networks.
- ❗keep SMB versions updated and secure shared network resources with strong authentication measures

### FTP and SFTP
File Transform Protocols (plaintext). SFTP secure file transfer via SSH.
- e.g. web developers using SFTP for file uploads and downloads

### RDP: Remote Desktop Protocol
Remote desktop control. 
- control Windows computers remotely
- ❗guard against weak RDP passowrds and open RDP ports (ransomware): MFA for secured remote work

### SNMP: simple network management protocol
Network monitoring and device management. 

***
**Email & Authentication Protocols**

### SMTP: simple mail transfer protocol
Send emails, transmit messages across internets

### IMAP: internet message access protocols
Allows users to read emails across multiple devices without downloading them. (stay synchronised)

### POP3: post office protocol 3
Downloads emails to a single device and removes them from the server (local access).

### LDAP: lightweight directory access protocols
centralised authentication systems
- many organisations use this (only employees can access emails)

***
**Wireless & network security protocols**

### WPA2
Encrypts Wifi connections, widely used security standard

### WPA3
Improved security for wifi, better protection against attacks.

### IPsec
Encrypts entire network traffic, used in VPNs.
- prevent third parties from monitoring online activities

### BGP: border gateway protocol
Routes internet traffic globally, ensures efficient data transmission
- routes between different networks on the internet
- determine most efficient path (optimal)

***
**Future and emerging protocols**

### QUIC: quick UDP Internet Connections
Faster internet browsing, low-latency connections, replaces TCP in many cases.
- aiming to replace TCP (multi-step handshake process)

### MQTT: message queueing telemetry transport 
Lightweight IoT messaging protocol, used in smart devices.
