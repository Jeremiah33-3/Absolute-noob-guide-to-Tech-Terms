## Links

1. Interview [questions](https://www.geeksforgeeks.org/category/computer-networks/)
2. OSI model [explanation](https://www.geeksforgeeks.dev/learn/SystemDesign/osi-model)
3. GeeksforGeeks [tutorial](https://www.geeksforgeeks.org/computer-networks/computer-network-tutorials/)
4. GeeksforGeeka [cheatsheet](https://www.geeksforgeeks.org/computer-networks/computer-network-cheat-sheet/)
5. GeeksforGeeks [interview corner](https://www.geeksforgeeks.org/interview-prep/interview-corner/)

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

***
**Future and emerging protocols**

### QUIC: quick UDP Internet Connections
Faster internet browsing, low-latency connections, replaces TCP in many cases.
- aiming to replace TCP (multi-step handshake process)

### MQTT: message queueing telemetry transport 
Lightweight IoT messaging protocol, used in smart devices.
