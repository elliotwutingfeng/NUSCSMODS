---
layout: post
published: true
title: 'CS3103 - Lecture 5: Socket API '
subtitle: Week 5 lecture socket programming
---
# Socket

![CS3103-5-1.PNG]({{site.baseurl}}/img/CS3103-5-1.PNG)

- Interface between the application layer and transport layer
- OS controlled interface into which application process can both send and recieve messages

Addressing: 
- Host address and process identifier
- Ip address + Port number


Socket is an endpoint for communication. A combination of host IP address and port number

## Socket types
![CS3103-5-2.PNG]({{site.baseurl}}/img/CS3103-5-2.PNG)

## UDP sever: Connectionless (Iterative)
![CS3103-5-3.PNG]({{site.baseurl}}/img/CS3103-5-3.PNG)

- All wil go to the same port
- ALl will go to the same queue

> We can pqaralised

## TCP server: Connection oriented (COncurrent)

![CS3103-5-4.PNG]({{site.baseurl}}/img/CS3103-5-4.PNG)


- Create a seperate child process
- Child process may use same or new port
- The port is that dedicated to that client
- The next client will then go to the next child server
- Given that each socket is identified by local ip and port and remote ip and port, no need for emphemeral port at server sides (Uniquely identifieable) 
- Can be iterative but now majority are concurrent

## Socket Data structure
![CS3103-5-5.PNG]({{site.baseurl}}/img/CS3103-5-5.PNG)

## UNIX LINUX SOCKET API (C/C++)

#### Creating a socket
- `sockDes = new Socket(pf, type, protocol)`
	- pf : protocol family
    - type : SOCK_STREAM for TCP, SOCK_DGRAM for UDP, SOC_SEQPACKET for sctp, SOCK_RAW only for priviledge programs
    - Protocol : Is always 0 by default.. There was suppose to be more protocol but until it still the same
    
    

#### Binding
- `bind(sockDes, localaddr, addrlen)
	- socket will have a wild card foreign destination
    - localaddr is pointer to a structure defined in socket.h which specifies the local socket address 
    
![CS3103-5-6.PNG]({{site.baseurl}}/img/CS3103-5-6.PNG)

### UDP Server
1. sockDes = new Socket(pf, type, protocol)
2. bind(sockDes, localaddr, addrlen)
	- socket will have wild-card foreign destination; foreign addr is yet to be assigned
3. rescfrom(sockDes, buffer, length,flags, fromaddr, addrlen)
	- OS will record the fromaddr and addlen based on datagram recievedf
4. sendto(sockDes, message, length, flags, destaddr, addrlen)
5. close(sockDes)


### UDP Client
1. sockDes = new socket(pf, type, protocol)
2. sendto(sockDes, message, length, flag, destaddr, addrlen)
3. recvfrom(sockDes, buffer, length, flags, fromaddr, addrlen)
4. close(sockDes)

> Bind is optional.. our client could take a random port address


### TCP Server
1. sockDes = new socket(pf, type, protocol)
2. bind(sockDes, localaddr, addrlen)
	- socket will have wild-card foreign destination; foreign addr is yet to be assigned
3. listen(sockDes, qlength)
4. newSockDes = accept(sockDes, addr, addrlen)
	- new socket will have requesting client as dest and returns newSockDes to server, connection is establised to specific client
5. read/write(newSockDes, buffer, length)
6. close(sockDes); close(newSockDes)

### TCP Client
1. sockDes = new socket(pf, type, protocol)
2. connect(sockDes, destaddr, addrlen)
3. read/write(sockDes, buffer, length)
4. close(sockDes)


## Raw socket
![CS3103-5-7.PNG]({{site.baseurl}}/img/CS3103-5-7.PNG)



> See the slides for commands

# Slides
<iframe src="https://drive.google.com/file/d/1uVa8AoDjED1tb3r9yGctDhMPH-W7nUtJ/preview" width="640" height="680"></iframe>
