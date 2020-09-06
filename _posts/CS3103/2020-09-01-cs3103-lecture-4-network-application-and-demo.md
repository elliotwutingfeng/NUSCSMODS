---
layout: post
published: true
title: 'CS3103 - Lecture 4:  Network Application and Demo'
---
# Network application
- Client to server
- Peer to peer

#### Client server architecture
Properties of server:
- Always on host
- Uses ephemeral ports
- Uses perm IP address
- init communication
- Waits to be contacted

#### P2P
- No always on server
- Arbituary end systems directly communication and serve each other
	- Each host runs both server and client processes


> Question: What is the advantage of P2P
>
> - Everything is client and everything is server


> Question: How does host find the ip address of each other?
>
> - Easy to scale


#### Socket
- Interface between application layer and transport layer
- OS controlled interface ("door") into which application process can both send and recieve messages

Addressing:
- Host addr + process identifier
- IP add + Port number

> TOOL
> 
> - Use `ifconfig` (ubutun) or `ipconfig` (windows) to see edit your laptops IP address
> - Use `cat /etc/services` to see all well known port numbers

Socket: Endpoint for comm. A combination of host ip address and port numbers


#### Internet transport protocol services

TCP | UDP
--- | ---
Reliable transport between sending and recieving process | Unreliable data transfer between sending and recieving process
Flow control, sender wont overwhelm reciever | Does not provide reliabitly, flow control, congestion control, timing, throughout guarantee, security or connection setup
Does not providfe timing, minimum throughtput gurantee, security | 
Connection oreiented: Set up required between client and server processes |

> Question: Why bother? Why is there a UDP
>
> - 


#### Securing TCP

TCP and UDP:
- No encryption
- Cleartext passwords send into socket, traverse internet in cleartext

SSL:
- Provides encrypted TCP connection
- data integrity
- end point authentication


> SSL is at app layer: Apps use SSL libs which talk to TCP


# HTTP
- Use TCP service
- Stateless
	- Server maintains no info about past client requests
    - If server/client crashes, their views of state may be inconsistent
    
- Default port: 80


##### Non Persistance 
- Server terminates connection after transferring the file or object 
- HTTP 1.0 
- New connection is established each time (New set of TCP variables and buffers)
- Browsers often open parallel TCP connections to fetch referenced objects

Response time:
- One RTT to intiate TCP connection
- one RTT for HTTP requests and first few bytes of HTTP response to return
- file transmission time
- 2RTT + transmit time

> RTT time taken for a small packet from client to server and then back to client

##### Persistance
- Server leaves the TCP connection open after sending the response
- Subsequent requests between the same client and server will use the same connection
- WIthout pipelineing: One RTT for each object
- With pipelining: as little as One RTT for all referenced object
- Default in HTTP 1.1

### Message format
img
#### Request and response status line


### User state management: Cookies
- HTTP is stateless
- Use cookie to manage user identity
- Components:
	- HTTP response header (By web server upon init request from client)
    - HTTP Response header (Every subsequent request by client)
    - Cookie file is maintain by the browser
    - Back end database at website
    
    
### Web caches
The goal is to satisfy client requests without involving origin server. Improve response time and reduce traffic
- User sets browser
- Browser sends all HTTP request to cache
	- Objects in cache: Returns the object
    - Else cache request object from origin server and returns to client

# FTP
FTP use the services of TCP, it needs two TCP connection.


Port: 
- 21 : Use for control connection
- 20 : Data connection


> FTP server maintains the state about the user throughout the session: Current directory and earlier authentication

## FTP connection

ACTIVE MODE:


PASSIVE MODE:


## DEMO



# Email protocols

Components:
- User agent/Mail readers:
	- Eudora
    - Outlook
    - Pine
    - Mozilla thunderbird
- Message transfer agents
	- SMTP: SImple main transfer protocol
- Message access agents
	- POP3 => Post office protocol v3
    - IMAP4 => Internet Mail Access Protocol V4
  
#### Push vs pull

- PULL: TCP connection is intitiated by the machine that wants to recieved the file
- PUSH: TCP connection is initiated by the machine that wants to send a file

> What is HTTP THEN?
##### Format


## SMTP Example
## POP example


# DNS (Domain Name Space)
- The name consist of discrete elements that are related to each other usually using hierachical parent child semantics
- Easy to avoid conflicts

## Domain
A subtree of domain name space

DNS Components:
- Distributed database implemented in hierarchy of many name servers
- Application on top of UDP/TCP
	- Client or resolver
    - DNS Server application
    - DNS server port 53
    
> Why dont centralised DNS


If the size of the response message is more than 512 bytes, a TCP connection is used instead of UDP

## TLD
Top level domain servers:
- Responsible for com, org, net, edu ...etc 
- Network solution maintains servers for .com TLD
- Educause for .edu TLD

Authoritative DNS servers:
- Organisation own DNS server providing authroitative host name to IP mappings for organisation named hosts
- Can be maintain by organisation or service provider

## Local DNS name server
- Does not strictly belong to hierachy
- Each ISP has one
- When host makes DNS query, it is send to its local DNS server
	- Local has cahce of recent name to address translation pairs but might be out of date
    - Acts as a proxy and forwards query into hierarchy

## DNS name resolution example

## Domain and zone
The DNS server for a domain can either store info about every node in domain or divide the domain into subdomains and delegate part of its authoirity to other servers

> What a server is responsible for or has authority over is called a zone

## Primary and secondary servers
- Primary: Stores info about the zone in is an authority for
	- Creates maintains and updates zone files
- Secondary: Has complete info about a zone
	- Cannot create or update szone files
- Primary and secondary servers are both authoritative for the zone they serve. They provide authoritative answer for their zone.
	- An authroitative answer for a name server (Such as reading the data from disk) is guaranteed to be accurate
    - A non authoritative answer (Like from cache) may not be accurate
## Reource records

## Format of DNS replies

## Dynamic DNS
There might be changes in DNS when
	- Add new host
    - Remove host
    - CHange ip

Changes must be made to the DNS master file. THe file must be updated dynamically.

- Zone entries can be dyn updated in real time by DDNS client
- DHCP configured host with a well known and fixed and fully qualified domain name

## DNS tools


# P2P Applications


