---
layout: post
published: true
title: 'CS3103 - Lecture 3: IP - Options, ICMP'
---
# IP
![CS3103-3-1.PNG]({{site.baseurl}}/img/CS3103-3-1.PNG)

> Question: Why is there no Payload length?
> - total length - header length  can be use to figure out the payload length. The IP packet also might not alwyas be 20 bytes

The bits are transmissted row by row
- First transmit bits 0-7
- Then transmit 8-15
- then 16-23
- then 24-31

This is called network byte order or big endian byte ordering

> Note that many computers store 32 bit words in little endian format


#### Encapsulation of a small datagram in an ethernet frame

![CS3103-3-3.PNG]({{site.baseurl}}/img/CS3103-3-3.PNG)

The transmission shld be have a minimum length requirement so that we will be able to detect if there is a collision

#### Big datagram
![CS3103-3-2.PNG]({{site.baseurl}}/img/CS3103-3-2.PNG)

There is a need for maximum length requirement for ethernet due to avoiding corruption. Too big, if there is a corruption.. it will take v long to retransmit it.

## IP fragementation

![CS3103-3-4.PNG]({{site.baseurl}}/img/CS3103-3-4.PNG)

- Takes placde because of physical level limitation
- occurs at router or original sending host
- Reassembled at destination host

### Segmentation and Fragmentation

![CS3103-3-5.PNG]({{site.baseurl}}/img/CS3103-3-5.PNG)

TCP: 
- Divides them into segment base on the link layer 
- To avoid Fragmentation in the other layers

> Avoid fragmentation because if one fragment is corrupted, the entire thing must be retransmitted

![CS3103-3-6.PNG]({{site.baseurl}}/img/CS3103-3-6.PNG)

UDP:
- There is no segmentation
- There is a max size 
- It goes to IP layer, and it will check the link layer to see if need to ip layer fragementation
- UDP header is only added to the first fragment


> Length of the data in each fragment must be in multiple 8 (except for the last packet)
> - It is the size of a word

#### Question
1) If a packet has arrived with an M bit value of 2 and a fragmentation offset of 0. Is this first feag, last or middle?
> Middle, tseen through offset  = 0

2) A packet has arrived in which offset is 100, the value of Hlen is 5 and value of the total length field is 100. What is the number of first byte and last byte of the IP payload

>  Start: 8*100
> Offset from the start : 100 - 20 = 80 [Total length - Header size]
> End bit: 800 + 80 -1 = 879 (start from 0)

- The size of header is 5*4 where 5 is the value given in the header and 4 is the number of bytes
- Get the size of each payload by using MTU (Maximum Transmission Unit) - Header size
- Since offset bit is suppose to represent the fragment, we realised that the size of each payload might be too big for the offset (13 bits) to represent.. Thus we make it a multiple of 8 
	- e.g MTU: 1500 bytes
    - Total size of ip packet: 65536
    - Fragmets: 0, 1480, 2960...65120 as offset
    - 65120 cannot be represent as offset due to the lack of bits
    - Make it a multiple of 8: 1480/8 = 185
    - We have 0,185,330 instead
    
## Options

### Record Route Option
Concept:
### Strict source route Option

### Loose source route option

### IP components

# ICMP (IPV4)
- What if router cannot route to deliever datagram
- What if a router experience a congesting
- What TTL expire


Router needs to inform source to take action to avoid or correct problem. 
ICMP:
	- Allows router and hosts to send error or control messages to other routers or hosts
    - Error reporting mechanism and can only report condition back to the original source
    - ICMP is specified in RFC 792

#### Format
- 8 byte header, variable size data section
- Format for first 4 bytes of header is common to all ICMP packets
- Type: ICMP messgae type
- Code: Reason for the message type generated


## ICMP error messages

### ICMP error messages - Examples

- Source quench message: Informs the source that a datagram has been discarded due to congestion in router or the destination host
- Source must slow down sending of datagrams until congestion is relieved
- One message sent for each datagram discarded

## Query

ICMP can also diagnose some network problems through query messages, a group of four different pair of messages. In this type of ICMP message, a node sends a message that is answered in a specific format by the destination node

### ICMP query messages - Examples


## Traceroute program
Allow us to see the route that IP datagrams follow from one host to another

> Question: Based on what we known about ICMP, how should traceroute work?
> 
> - 


- Sends UDP datagram to destination with TTL field in IP Header set to value 1
	- Datagram = 40bytes
    - 12 bytes data = seq no, time sent
- Causes router to generate "time exceeded" ICMP error
- Increment TTL progressively until final destination is reach
- Terminating:
	- UDP port chosen is a non existence port
    - Destination sends ICMP "Port unreachable" error
- For each TTL value, 3 datagra,s (probes) are sent

> Question: Some firewalls disable UDP messages, is there an alt method?
>
> - 



> Question : Is there any diff between route info shown by Traceroute and IP record route?
>
> -




