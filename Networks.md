# Networks jargon 

coming up next

### Subnet

### Router

### Switch

### Gateway 

### TCP vs UDP

### HTTPS, TLS, HTTP, SSL

### DNS

### Rest API

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
