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
![CS3103-3-7.PNG]({{site.baseurl}}/img/CS3103-3-7.PNG)

#### Format
![CS3103-3-8.PNG]({{site.baseurl}}/img/CS3103-3-8.PNG)

We want to copy all the options from the first fragment to all the fragment


### Record Route Option
Record the route in which the packet is moving.

![CS3103-3-9.PNG]({{site.baseurl}}/img/CS3103-3-9.PNG)

- 40 bytes
- 9 address only


Concept:
A packet from network `67.0.0.0/24` to `138.6.0.0/16`

- Type field is set to 7 initially
- Pointer points to the byte in which the next empty address block is at

![CS3103-3-10.PNG]({{site.baseurl}}/img/CS3103-3-10.PNG)

The pointer might exceed, but the reciever will check the length to ensure that it doesnt go beyond what is needed

> If it exceeds 9 address, it cannot record the 10th add

### Strict source route Option
Follow the path defined by the sender which is denoted by the ipaddresses

![CS3103-3-11.PNG]({{site.baseurl}}/img/CS3103-3-11.PNG)

- Notice how it will swap the address of the destination and the list of ip address each time in moves forward to the next router

![CS3103-3-12.PNG]({{site.baseurl}}/img/CS3103-3-12.PNG)


> Normally ip packet will have final destination, but then in this case.. the destination packet is just the next hop that is stored in the list.


Purpose: We might want to check if a certain path exist, we can use this to test if such a path exist



### Loose source route option
![CS3103-3-13.PNG]({{site.baseurl}}/img/CS3103-3-13.PNG)

The packet can go to many other router before going to the ip written in this list


#### IP components
![CS3103-3-14.PNG]({{site.baseurl}}/img/CS3103-3-14.PNG)

# ICMP (IPV4)
- What if router cannot route to deliever datagram
- What if a router experience a congesting
- What TTL expire


Router needs to inform source to take action to avoid or correct problem. 
ICMP:
	- Allows router and hosts to send error or control messages to other routers or hosts
    - Error reporting mechanism and can only report condition **back to the original source**
    - ICMP is specified in RFC 792
    
SDN: Software defined network, let the programmer decide the software stuff so remove all the software within the switch and the routers
e.g Everything is dynamically programmed



Network layer:
![CS3103-3-15.PNG]({{site.baseurl}}/img/CS3103-3-15.PNG)

- ARP is not really used
- ICMP message goes into IP data
- It is then put into ethernet frame and then tranmitted

> ICMP message is encapsulate in the ip header which is why it is at the top of the network layer. 

#### Format

![CS3103-3-16.PNG]({{site.baseurl}}/img/CS3103-3-16.PNG)

- 8 byte header, variable size data section
- Format for first 4 bytes of header is common to all ICMP packets
- Type: ICMP message type
- Code: Reason for the message type generated

## ICMP MESSAGES
- Error reporting message
- Query
![CS3103-3-17.PNG]({{site.baseurl}}/img/CS3103-3-17.PNG)


## ICMP error messages

![CS3103-3-18.PNG]({{site.baseurl}}/img/CS3103-3-18.PNG)

Recieve datagram: 
- Might be final or not
- Some error happens, i need to report back
- Create ICMP packet


ICMP Packet:
- Payload: The received datagram header (inc ip address) and first 8 byte of payload copied
- Adds whole thing into ip packet
- Sends back to source


> Question: Why is IP header of recieved datagram included in error message
> 
> - IP header in the IP datagram has the source and dest of the router which is sending the error message. 
> - The sender needs to know who is the prev destination which the failed packet suppose to be send to
> - Check that you are the correct recipient of the ICMP. Along the way.. the source might be corrupted



> Question: Why 8 bytes of the recieved datagram is included in the reply?
>
> - TCP IP  (not full) / UDP header
> - Know which packet cause the error



#### Example
ICMP error messages are use by router and host to tell a device that sent a datagram about problems

1) What if datagram carring ICMP cause another error
> Nothing happne, it wont be sent again

2) Do we need ICMP error messages for each fragment of a fragmented datagram that cause the error
> Only for first

3) ICMP will not be generated for a datagram having a multicast or broadcast add in destination add field. Why?
> Broadcast storm, one messaege will be split into many and routers would have made multiple copies of the packets. (Lots of destination)

4) ICMP error messages will not be for a datagram whose source address is not a single host, 0.0.0.0, 127.X.X.X , broadcast or multicast add. why?
> If source is any of those, it not meaningful
>
> - Broadcast/multicast: Not meaningfukl
> - 0.0.0.0 : for starting out

![CS3103-3-19.PNG]({{site.baseurl}}/img/CS3103-3-19.PNG)
> Protocol: The transport layer is not there


> Question: Who generates these ICMP error messages, host or routers?
>
> - Both, depending on the codes



### ICMP error messages - Examples

##### Source quench:
![CS3103-3-20.PNG]({{site.baseurl}}/img/CS3103-3-20.PNG)
- Send back to the source


- Source quench message: Informs the source that a datagram has been discarded due to congestion in router or the destination host
- Source must slow down sending of datagrams until congestion is relieved
- One message sent for each datagram discarded

##### Time exceeded:
![CS3103-3-21.PNG]({{site.baseurl}}/img/CS3103-3-21.PNG)

- When every a router decremenets a datagram with a TTL value to zero, it discard the datagram and sesnds the time exceeded message to original source
- When final destination does not recieved all the frag in a set time, discards the received frag and sends the ttl exceed message

> A host usually starts with a small routing table that is gradually updated and augmented. 

##### Redirction:
![CS3103-3-22.PNG]({{site.baseurl}}/img/CS3103-3-22.PNG)

The first router normally recieves a packet from an interface and sends it in another interfacfe. If the recieves the same packet from the same interface it recently sents.. it will sent redirection "RM", the host will then update its table base on this infomation


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
