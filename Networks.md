# Networks jargon 

coming up next

### JWT Token and Session

### Cookie

### Subnet

### Router

### Switch

### Gateway 

### Rest API

### RPC
> Remote Procedure Call is a framework/[architectural style](https://aws.amazon.com/compare/the-difference-between-rpc-and-rest/?nc1=h_ls) for APIs, which are mechanisms used to enable 2 softwares componnets to communicate with each other using a set of protocols/definitions. RPC's biggest feature is that it allows developers to call remote functions on external servers as if it was local.

- different from REST, REST allows developers to perform specific data operations on the remote server, and it is a set of rules instead of a system/framework
- RPC: function call is made on the client side using HTTP POST while the actual function is invoked on the server side; client must know the function name and parameters
- however, REST usings HTTP verbs/methods to perform data operation, through server resource URLs, without the need to know the specific function names on the server; more standardised methods
- [gRPC](https://www.youtube.com/watch?v=gnchfOojMk4) is gaining popularity

### TCP vs UDP
> [TCP](https://www.geeksforgeeks.org/what-is-transmission-control-protocol-tcp/): transmission control protocols (TCP/IP network): connection-oriented protocol for communications that helps in the exchange of messages between different devices over a network
- must first acknowledge a sesssion between the two computers that are communicating (verification)
  - by sending SYN first, then SYN ACK, then send back ACK RECEIVED -> then data can be delivered (starts communication)
- gurantees delivery of data (will resend if data go astray)
> [UDP](https://www.geeksforgeeks.org/user-datagram-protocol-udp/): User Datagram Protocol: connectionless-oriented protocol
- it does not establish a session and does not gurantee data delivery
- less overhead and latency --> faster connection than TCP (for games and video communication) 

### HTTPS, TLS, HTTP, SSL
> HTTP: used for viewing webpages on the internet
- all information is sent in clear text (transferred over public internet), therefore it is vulnerable to hackers (clear text)
- not good for transferring sensitive data
> HTTPS: secured HTTP, HTTP with a secured feature
- encrypts the data that is bein retrieved by HTTP -> ensures that all the data that is transferred is secured through encrypted algorithms (encrypted text)
***HTTPS can use either of the below secure protocols to encrypt its data***
> SSL: secure sockets layer is a protocol that is used to ensure security on the internet; uses public key encryption to secure data
- SSL encrypts the link between a web server and a browser which ensures that all data passed between them remain private and free from attack.
- Working architecture
  - computer connects to a website that is using SSL
  - computer web browser asks the website to identify itself
  - web server sends it a copy of the SSL certificate (a certificate used to autheticate the identity of a website, for trustworthiness used)
  - trusted then computer browser will send a message to website, the server will respond back with an acknowledgeablement so an SSL session can be established
  - now encrypted data can be exchanged between computer and web server
> Transport layer security: similar to SSL (based on the same specifications), like SSL also autheticates server, client then exchange encrypted data
- latest industry standard cryptographic protocol, a successor to SSL

### [DNS](https://www.geeksforgeeks.org/whats-is-domain-name-systemdns/)
> translate human-readable domain name into IP address (phone book) 

### [Port](https://youtu.be/g2fT-g9PX9o?si=fLGM2XCPdfw0IZcG)
> Port is a logical connection that is used by programs and services to exchange information. It is not a physical connection.
- it specifically determines which program or service on a computer or server that is going to be used (e.g. pulling up a webpage, accessing email)
- unique identification number (0 - 65535)
  - fun fact: limitation of 65535 ports -> TCP protocol allows only 16 bits that can be encoded to be a port number

### IP address
> an numeric address that serves as an identifier for a computer or device on an network.
- for communication purposes
- determines the geographical location of the server

### FTP
> file transfer protocol: standard protocol used to transfer files (between computers and servers) over a network
- [difference with http](https://www.geeksforgeeks.org/difference-between-ftp-and-http/)
  - both are set of rules that determines certain connections and communications but HTTP (hypertext transfer protocols) deals mainly with transferring of webpages while ftp deals with transferring of files (uploading and downloading on a computer over the internet) 
  - files transferred via http are not saved in memory but that of ftp are.
  - http is stateless but ftp maintains states
  - http is a one way communication system (server sends required webpages to client's browser) but ftp is a two way communication (server upload files, client download files)

### API
> application programming interface are mechanisms that enable two software components to communication with each other using a set of definitions and protocols.
- architecture pivots on client-server, where client sends request, server responds

### Netstat
> Network statistics: command line tool that is used to display the current network connections and port activity on your computer
