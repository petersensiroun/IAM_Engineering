# **<u>IP Addresses:</u>** 

**IP Address -** is a unique identifier for a device on a network. It allows devices to find and communicate with each other 

**IPv4 -** 32 bit. written as four numbers separated by dots (192.168.1.10) It is split into four 8-bit sections called **octets** , separated by dots. Each octet can hold a number from **0 to 255** ( each octet is 8 bits) 

**Private IP -** used inside of local networks, not routable to the public internet 

- 10.0.0.0 - 10.255.255.255 (10.0.0.0/8) 

- 172.16.0.0 - 172.31.255.255 (172.16.0.0/12) 

- 192.168.0.0 - 192.168.255.255 (192.168.0.0/16) 

**Public IP -** everything else that's routable on the internet 

**CIDR -** Classless Inter-Domain Routing 

Allows flexible IP address allocation by enabling subnetting at various points preventing the waste associated with fixed class systems – optimizes limited IPv4 address space 

**Suffix -** /24; how many bits are used for the network portion 

The binary 192.168.0.1  = <mark>11000000.10101000.00000000.00000001</mark> The suffix /24 = the first <mark>24</mark> bits are for the network, the remaining 8 are for host 

# **<u>Subnets</u>** 

**Subnet -** a smaller network of computers connected to a larger network through a router. It divides a network into 2 or more subnets. 

- A subnet can have its own address system so computers on the same subnet can communicate quickly and securely without sending data across the larger network 

- IP addresses have 2 parts: network and host. 

   - Network identifies the overall network 

   - Host identifies the device 

## **Why Do Subnets Matter For Cloud Access:** 

Subnets form foundational geographic and logical boundaries where network-level security controls and routing rules are enforced. 

**Network-Level Filtering (NACLs) -** firewalls like security groups control traffic at the individual virtual machine level, NACL’s operate as stateless traffic filters at the subnet level **. A policy applied to a subnet instantly protects every resource placed inside that IP address range** 

**Public vs. Private -** subnet access is defined by its route table attachment to gateways ( like internet gateway). Placing a resource in a private subnet inherently blocks direct inbound access from the public internet, acting as broad compliance access policy by default 

**Availability Zone Isolation** -  Subnets map to single Availability Zones (AZs). Access policies and architectures use this mapping to restrict failure domains or enforce high-availability compliance by keeping sensitive data tiers isolated across specific physical zones 

**Predictable IP and Traffic Management -** Dedicated subnets for specific infrastructure tiers prevent IP address exhaustion and route conflicts, making audit logs and security policy scopes much cleaner and easier to manage 

# **<u>DNS</u>** 

**DNS -** Domain Name System; the phonebook of the internet 

## **8 Steps in DNS Lookup:** 

1. <u>example.com</u> is typed into a web browser and the query travels into the internet and is received by a DNS resolver 

2. Resolder queries a DNS root nameserver (.) 

3. root server responds to the resolver with the address of a TLD (.com) 

4. Resolver makes a request to .com TLD 

5. TLD server gives IP address of the domain nameserver, <u>example.com</u> 

6. Recursive resolver sends query to domains nameserver 

7. IP address for <u>example.com</u> is then returned to the resolver from the from the nameserver 

8. DNS resolver responds to the web browser with the IP address of the domain initially requested 

9. Browser makes a http request to the IP address 

10. Server at the IP returns the webpage to be rendered 

## **Why DNS is Important for SSO:** 

**SSO -** Single sign on 

SSO relies heavily on the DNS to function securely and smoothly. SSO involves transferring sensitive authentication data across different domains, it needs a robust foundation of trust, security and routing, all managed through DNS 

# **<u>HTTP/HTTPS</u>** 

**HTTP -** Hypertext Transfer Protocol. When you open a website, your device is having a conversation with a server. 

**HTTP methods -** tells the server what action the client wants to perform on a resource. 

**HTTP Headers -** value pairs that travel along a request or response and provide extra context 

**TLS -** Transport Layer Security. Encrypts data sent over the internet to ensure hackers are unable to see what you transmit. Useful for sensitive info like passwords, credit cards, etc 

## **3 Main Components:** 

**Encryption -** hides data being transferred from third parties 

**Authentication -** ensures that the parties exchanging information are who they claim to be 

**Integrity -** verifies that the data has not been forged or tampered with 

**TLS Certificate -** for a website or application to use TLS it must have a TLS certificate installed on its original server. It’s issued by a certificate authority 

# **<u>Ports</u>** 

**Port -** tied to a location in memory running code. It's a conceptual address for networking programs to talk to each other. If IP is the street address that guides data to the correct device, a port is like the specific suite or room number that delivers the data to the right program inside of the device 

## **Port Categories:** 

**Port 0 - 1023** : **system** or well known ports ( 80, 443, 25,21) 

**1024 - 49151: User** or registered ports. Ports that can be registered by companies and developers for a service. 

1102 - Adobe Server 

1433 - Microsoft SQL Server 

**49152 - 65535: Dynamic or Private ports** . Ports client computers assign temporarily to itself during a session. Ex viewing a webpage 

System and User ports are used on a server. Private ports are used on a client. When my computer wants to use a service or program on a server, it assigns a  Private port 

## **Common Ports:** 

80, 443 - Web pages (HTTP, HTTPS) 20, 21 - FTP (File Transfer Protocol) 22 - standard TCP ( Transmission Control Protocol) for SSH (Secure Shell) 25 - Email (SMTP - Simple Mail Transfer Protocol) 

53 - DNS 

123 - NTP (Network Time Protocol) 179 - BGP ( Border Gateway Protocol) 587 - Modern SMTP with encryption 

3389 - RDP (Remote Desktop Protocol) 

389 - LDAP (Lightweight Directory Access Protocol) Allows user authentication 

636 - LDAPS - (LDAP over TLS) Encrypts traffic, operates over TLS 

Full list: full list 

# **<u>Flow of The Request:</u>** 

**1. Browser starts the request** 

**2. DNS Lookup** 

   - a. Pc asks a DNS server like a phonebook to translate into an IP address 

**3. Connecting via TCP and TLS Handshakes** 

   - a. TCP Handshake - Browser uses a three way handshake ( SYN, SYN-ACK, ACK) to open a reliable communication channel 

   - b. TLS Handshake - if the site is HTTPS, an extra handshake verifies the servers identity and creates an encrypted key for privacy 

**4. Sending HTTP Request** 

   - a. Browser builds HTTP request message (with GET or POST) containing headers with details like browser type and cookies 

   - b. Request breaks down into small data packets and travels across physical internet cables and routers to the target server 

**5. Server Processing and Database Work** 

   - a. Web server receives incoming packets and reads the request 

   - b. If page needs stored data (user profiles for product lists) the server queries a database server to fetch the information 

   - c. Server 

**6. Response Travels Back to the Browser** 

   - a. Server sends an HTTP response code - 200 along with website files back across the internet in data packets to clients device 

## **7. Browser Rendering** 

- a. Browser receives data packets, reassembles them, and parses HTML to build the DOM (Document Object Model) 

- b. Fetches extra resources like images or style sheets and paints the final visible webpage on the screen 

