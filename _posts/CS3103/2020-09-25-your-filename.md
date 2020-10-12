---
layout: post
published: true
title: CS3103 - Experiment 5
---

# Experiment
<iframe src="https://drive.google.com/file/d/1-uFlqnKu6lMLxCzeNEvTET417qYahQQb/preview" width="640" height="880"></iframe>

# Reading (Foruzans)

ICMP messages are divided into two broad catergoies: 
- Error reporting messsages : Reports problems that a router or host may encounter when it process an IP Packet
- Query messages: Occurs in pairs, help a host or network manager get specific info from a router or a host

![CS3230-lab-5-11.PNG]({{site.baseurl}}/img/CS3230-lab-5-11.PNG)

## ICMP Format
![CS3230-lab-5-1.PNG]({{site.baseurl}}/img/CS3230-lab-5-1.PNG)

### Error reporting messages
Although technology has produced increasingly transmission media, errors still exist and must be handle. Error checking and error control are not a concern of IP. ICMP just report errors.

> ICMP always reports error messages to the original source

Types:
- Destination unreachable
- Source quench
- Time exceeded 
- Parameter problems
- Redirection

Important points:
- No ICMP error message will be generated in response to a datagram carryig a icmp error message
- ICMP does not handle fragmentation (Doesnt care about second fragment)
- No ICMP error message will be generated for a datagram having a multicase address
- No ICMP error message will be henerated for datagram having a special address

> The data in the icmp packet contain the datagram of the first 8 bytes of the failed packet. (This is because the ports are stored there for the failed packet)

### Destination unreachable
When a router cannot route a datagram or host the datagram is discarded and router or host sends a destiantion unreachable message back to the source host.

![CS3230-lab-5-2.PNG]({{site.baseurl}}/img/CS3230-lab-5-2.PNG)

> Only codes 2 (port unreachable) and 3 (protocol unreachable) can be created by the destination host

Even if the router doesnt report, does not mean that datagram has been delivered.

### Source Quench
There is no communication between source host and routers which forwards it to the destiantion host. One of the ramifications of this absence of communication is the **lack of flow control and congestion control.**

- When host discards datagram due to congestion = source quence
1. Informs the source that datagram has been discaerded
2. Warns the source that there is congestion somewhere and the source should slow down (quench) the sending process

### Time exceeded
Genereated if:
- There are one or more errors in the routing table (Visit a series of router endlessly)
- All fragments that make up a message do not arrive at the destination host within a certain time limit given the first has already arrive

> Code 0 is used by router (Value of ttl is 0). Code 1 use by destination host (Not all fragment arrive at time)

### Parameter problem
- Ambiguitivy in the header part of datagram

> 0 : Error (Returns a pointer to show wheres the error)
> 1 : Missing

### Redirection
- To tell the host to upate its routing table to another router so that in the future, the host will send to that router rather then itself

![CS3230-lab-5-3.PNG]({{site.baseurl}}/img/CS3230-lab-5-3.PNG)

## Query
- Echo request and reply
- Time stamp request and reply

A node sends a message that is answered in a specific format by destination node

### Echo request and reply
- Diagnostic purpose
- Identifiy netowkr problems
- Determines whether two systems can communicate

> Echo request can be sent by a host or router, an echo reply message is sent by the host or router than receives an echo request message


The echo request and echo reply messages can be use to determine if there is communication at IP level. 

### Timestamp request and reply
- Determine ther round trip time for the ip datagram to travel between them
- Syncronise the clock machines

The source creates timestamp request message:
- Fills original timestamp field with UT by its clock
- Other time stamps are 0


Destination creates reply:
- Copy the original timestamp into reply timestamp
- Recieve: timestamp is destination's ut clock when receive
- Transmit: when datagram is send back

The source then takes care of the return time (When i recieve the packet from the destiantion)


- Sending time = recieve timestamp - original time stamp
- Receiving timee = return time - transmit timestamp
- Roundtrip time = Sending time + receiving time

> Round trip calculaation means the differences are cancelled out

Time difference = recieve timestamp - (Original timestamp field + oneway time duration)

# CheckSum

![CS3230-lab-5-5.PNG]({{site.baseurl}}/img/CS3230-lab-5-5.PNG)

# Debugging tools
- Ping
- Traceroute/Tracert(Windows)
	- Use time exceeded and destiantion unreachable (2) ICMP packets

# ICMP Package
![CS3230-lab-5-6.PNG]({{site.baseurl}}/img/CS3230-lab-5-6.PNG)

## Input model
- Handle all ICMP messages **recives**
- Invoke when ICMP pakcet is deliever to it IP layer
- Request: creates replu
- Redirect: Update routing table
- Error: Infoms the protoccol

## Output model
- Creating request, solicitation, or error messages
- Module receives a demand from IP, UDP, TCP
- Check if its allowed request
	- Cannot be created for:
    	- ICMP error
        - Fragmentaed IP packe
        - Multicst IP packet
        - IP packet having IP address 0.0.0.0 or 127.X.Y.Z
