---
layout: post
published: true
title: CS3103 - Experiment 5
---

# Reading (Foruzans)

ICMP messages are divided into two broad catergoies: 
- Error reporting messsages : Reports problems that a router or host may encounter when it process an IP Packet
- Query messages: Occurs in pairs, help a host or network manager get specific info from a router or a host

![CS3230-lab-5-11.PNG]({{site.baseurl}}/img/CS3230-lab-5-11.PNG)

## ICMP Format
![CS3230-lab-5-1.PNG]({{site.baseurl}}/img/CS3230-lab-5-1.PNG)

## Error reporting messages
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

## Destination unreachable
When a router cannot route a datagram or host the datagram is discarded and router or host sends a destiantion unreachable message back to the source host.

![CS3230-lab-5-2.PNG]({{site.baseurl}}/img/CS3230-lab-5-2.PNG)



