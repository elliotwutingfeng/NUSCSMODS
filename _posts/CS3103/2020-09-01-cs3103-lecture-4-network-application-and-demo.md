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

![CS3103-4-1.PNG]({{site.baseurl}}/img/CS3103-4-1.PNG)

Port: 
- 21 : Use for control connection
- 20 : Data connection


> FTP server maintains the state about the user throughout the session: Current directory and earlier authentication

The control command in the FTP is perm but for each file transfer, the current data connection will be close. A new data connection is needed to transfer the next file. 

> Control commands: "Out of Band" 
> Http is "In band"

FTP is stateful: 
- FTP maintains the user state until the user terminates the session

- Resolving heterogeneity between client and server
![CS3103-4-2.PNG]({{site.baseurl}}/img/CS3103-4-2.PNG)

File type:
- ASCII file 
- Image file

Data structure:
- File strcuture, record structure and page structure

Transmission modes:
- Stream mode, block mode and compressed mode

> Difference in file types, encryption types, datastrcuture between the client and server


FTP would convert the files into the proper format for the server/client can read

## FTP connection

ACTIVE MODE:
1. Control connection to port 32
2. client select arb port num
3. Informs the server 
4. Server use port 21 to connect to clients data port

![CS3103-4-3.PNG]({{site.baseurl}}/img/CS3103-4-3.PNG)

> However, sometimes incoming ports are blocked by firewalls.
> 
> - Let the client init the data connection instead of the server
> - In this image you can see that the server makes the connection..


PASSIVE MODE:
1. Client informs the server passive mode
2. Server open arb port for data connection
3. Informs the client that it has open a port and waiting for its connection
4. Client initaites the data connection

![CS3103-4-4.PNG]({{site.baseurl}}/img/CS3103-4-4.PNG)

> This solves the firewall

## DEMO
1. Telnet to connect to ftp
`telnet mirror.nus.edu.sg 21`
- default ftp is 21

Output
![CS3103-4-5.PNG]({{site.baseurl}}/img/CS3103-4-5.PNG)

2. Type in user and password 
> In this case it can be anoymous since the sch server configured it too

Response:
`230 Login successful`

3. Commands
- `PWD` :  check current directory
- `CWD /pub/apache` : CHange director

> If there is a - it means there is a continuation for the status. the last part shld not have a -
- `PASV`: tell server you want passive
- `EPSV`: external passive mode, waiting for another connection to the given port num
- `LIST`: File directory list transfer (passive or active must be configured first)

4. Connect to using another 
- `telnet mirror.nus.edu.sg <port given from 3.>`
- `LIST`

> Please note that the connection will close after awhile

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

![CS3103-4-6.PNG]({{site.baseurl}}/img/CS3103-4-6.PNG)

MTA client establish a connection to the server and pushes the message to the senders mail server. 
- It is queued for transfer to destination
- This follows smtp protocol
- Client server connection between MTA server at the reciever server.
- The message is psuh form the sender server to the reciever server


#### Push vs pull
![CS3103-4-7.PNG]({{site.baseurl}}/img/CS3103-4-7.PNG)

- PULL: TCP connection is intitiated by the machine that wants to recieved the file
- PUSH: TCP connection is initiated by the machine that wants to send a file

> What is HTTP THEN?
> - Can be classified as PULL as most of the time the client connects to the server to retrieve the file from the server


What are the additional components needed to send mail from Bob to Alice in the image/

#### User agent
![CS3103-4-8.PNG]({{site.baseurl}}/img/CS3103-4-8.PNG)

##### Format
![CS3103-4-9.PNG]({{site.baseurl}}/img/CS3103-4-9.PNG)

> why isnt there a format for FTP

1. Envelopes (Yellow)
- Location
- Use to route to the reciever

2. Message (blue)
- header
	- header name
    - reciever name
    - date
- body
	- Content to be sent to the reciever
![CS3103-4-10.PNG]({{site.baseurl}}/img/CS3103-4-10.PNG)

### Web based
![CS3103-4-12.PNG]({{site.baseurl}}/img/CS3103-4-12.PNG)


- Are actually http based
- Changes
	- Not SMTP from sender to mail server: HTTP
    - Not POP3/IMAP3 between mail to reciever at the end: HTTP

## SMTP Example
- Connect: `telnet smtp.nus.edu.sg 25`
- Details : `EMLO nus.edu.sg`
- Login: `AUTH LOGIN <UserID IN BASE64 FORMAT` > `<PASSWORD IN BASE64>`
- Write mail: 
			   MAIL FROM: `<EMAILADD>`
               RCPT to: `<RecieverADD>`
               DATA
               from: Alice
               to: Bob - to another account
               Hello this is a test mail
               .



- Close connection: `quit`

## POP example


## POP3 and IMAP
POP3:
- Previous example use POP3 download and delete mode
- POP3 download and keep copies of message on different client
- POP3 is stateless across session


IMAP:
- Keeps all messages in one place, server
- Allows user to org messages in folders
- Keep user state accorss session

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
- No always on server
- arbitrary end system directly communicate and serve each other
	- Each host runs both server and client processes

Examples:
- file distribution 
- streaming
- VoIP
- multiplayer games


> Question: What is the advantage of P2P?
>
> - Scalability


> Question: How the host find the IP addresses of each other?

## File distribution: Client server vs P2P
> How much time to distribute file from one server to N peers

- Server transmission: Must be sequentially send N file copies
	- Time to send one copy: F/us
    - Time to send N copies: NF/us
    
- Client: Each client must download file copy
	- dmin = min client download rate
    - min client download time: F/dmin
    
    
## File distribution: P2P
- Server transmission: Must upload at least one copy
	- time to send one copy: F/us
- Client: Each client must download file copy
	- min cleint download time: F/dmin
- clients: as aggregate must download NF bits
	- max upload rate (limiting max download rate) is us + Sum of ui


### Client server vs P2P: example

## P2P file distribution: BitTorrent (BT)
- file divided into 256Kb chunks
- peers in torrent send/recieve file chunk



As a leecher download pieces of the file, replicas of the pieces are created. More downloads means more replicas available. 


As soon as a leecher has a complete piece, it can potentially share it with other downloaders. Eventually each leecher becomes a seeder by obtaining all the pieces and assembles the file. Verifies the checksum

## BitTorrent: Requesting, sending file chunks
Requesting chunks:
- At any given time, different peers have different subset of file chunks
- periodically, Alice ask each peer for list of chunks that they have
- Alice requests missing chunks from peers
- Requires - Piece selection policies:
	- the order in which pieces are selected by different peers is criticals for good performance
    - If an inefficient policy is used, then peers may end up in a situation where each has all identical set of easily available pieces and none of the missing ones.
    - If the original seed is prematurely taken down, then the file cannot be completely downloaded
    > What are good policies
## Piece selection

- Strictly priority 
- Random first piece
- Rarest first 
- Endgame mode


Random first piece

- initally a peer has nothing to trade
- important to get a complete piece asap
- select random piece of the file and download it


Rarest piece first
- Determine the piece that are most rare among your peer, and download those first
- Logically, the most commonly available piece are left till the end to download


Endgame mode
- Near the end, missing pieces are requested for every peer containing them
- This ensures that a download is not prevented from completion due to a single peer with a slow transfer rate
- Some bandwidth is wasted, but in practice this is not too much

#### Choking
- Choking is a temporary refusal to upload to free riders. It one of BT's most powerful idea to deal with free riders (those who only downlaod but never upload)
- tit for tat strategy is based on game theoretic concepts

## BitTorrent: Requesting, sending file chunks
Sending chunks: tit for tat
- Alice sends chunks to four peer currently sending her chunks at highest rate
	- other peers are choked by Alice (do not recieve chunks from her)
    - re-evaluate top 4 every10 secs
- Every 30 secs: randomly selects another peer, starts sending chunks
	- Optimisitcally unchoked this peer
    - Newly chosen peer may join top 4

### Tit for tat

### Upload-Only mode
- Once download is complete, a peer can only upload. The questions is, which nodes to upload to?
- Policy: Upload to those with the best upload rate. The ensures that pieces get replicated fastern and new seeders are created fast


### Simple database: DRe-centralised

### HashTable: De centralised
- More convenient to store and search on numerical representation of key
- key = hash(original key)

### Distributed Hash Table (DHT)
- Distributed(key,value) pairs over millions of peer
	- Pair are evenly distributed over peer
- Any peer can query database with key
	- database returns value for the key
    - To resolve query, small number of messages exchanged among peer
- Each peer only knows about a small number of other peers
- Robust to peer coming and going (churn)


