---
layout: post
published: true
title: 'CS3103 - Lecture 2: ARP, DHCP, VLAN'
---
# ARP - Address Resolution Protocol
![CS3103-2-1.PNG]({{site.baseurl}}/img/CS3103-2-1.PNG)

Motivation:
- Support hop to hop deliever

![CS3103-2-2.PNG]({{site.baseurl}}/img/CS3103-2-2.PNG)

- Ip output send some packet out, it will then check if its multicast or broadcast
	- Multicast/Broadcast: Put on ip input queue
    - Not: Next step
- IP destination = Local IP?
	- Yes: Put on IP queue
    - No: Get mac address with ARP
- ARP
- Demux it: Knows it ipv4 or ipv6
- Sents to approp layer
- Put on input queue

> Multicast must be registered to get the message but broadcast is already automatically sent no matter what

## Address Translation with ARP

### ARP Request: Broadcast
- Client would broadcast requesting for the MAC address of a node (ARP request)


ARP broadcast is restricted to within a LAN

### ARP Reply: Unicast
- Node replies with the hardware MAC address
- Other nodes ignore
- client would store the MAC address in its cache

![CS3103-2-3.PNG]({{site.baseurl}}/img/CS3103-2-3.PNG)
Note: There is a typo with the IP address, it shld be 128.143.71.1 for router137

Arp cache contains address mapping for all host within a single LAN

> ARP cache will go two ways

## ARP Packet Format

![CS3103-2-4.PNG]({{site.baseurl}}/img/CS3103-2-4.PNG)

- Hardware type: Mac layer type (Ethernet/Wireless LAN)
- Protocol type: IP layer type
- Operation code: Reply or request

#### ARP Example
![CS3103-2-5.PNG]({{site.baseurl}}/img/CS3103-2-5.PNG)

> Note that if i dont know the reciever MAC, i would leave as 0

> Question: If they broadcast and the destination is not for me, would I update the arp cache?
	- Yes, only if I already have a exisiting entry, i will update else i will throw

> Question: What is the purpose of having variable length address as Source/Target hardware address/Protocol
	- For future expansion

## Proxy ARP
Host or router responds to ARP request that arrives from its connected networks for a host that is on another side of its connected networks

![CS3103-2-6.PNG]({{site.baseurl}}/img/CS3103-2-6.PNG)


> Question: When will you use proxy arp?
	- When we are moving the packet to another subnet, we can use a router as a proxy arp. 
    - It is also used as a short cut to connect two different networks without changing it.

## Things to know about ARP
- What happens if an ARP request is made for a nonexisting host
  - Time out
- ARP cache might refreshes and a host periodically sends ARP request for all address listed in ARP cache
- Gratuitous ARP request: A host sends an ARP request for its own IP address
	- Check if its own IP address is assigned to somewhere else.. If it is, the other host will reply. 

## Vulnerabilities of ARP
1. ARP does not authenticate request or replies, it can be forged
2. ARP is stateless: It can be sent without a request
3. All nodes when recieves a IP address that already has an entry, it should update

> ARP Poisoning, the arp cache is tainted with bad pairings


# DHCP - Dynamic Host Configuration Protocol

Allows allocation of IP address from a pool
   - Static: For routerm server
   - Auto: indefinite time
   - Dynamic: Specific duration, loans IP addresses for a limited time

It is a UDP base application

#### ARP vs DHCP
![CS3103-2-7.PNG]({{site.baseurl}}/img/CS3103-2-7.PNG)

- DHCP: App Layer
- ARP: Network


> DHCP is a application layer as it is design at a later stage at the application part thus it is consider to be in this layer

## Client - Server Interaction

### DHCPDISCOVER
![CS3103-2-8.PNG]({{site.baseurl}}/img/CS3103-2-8.PNG)

- DHCP server will select some ip address to give to the client

> Question: What is the use of the ping probe
	- To check if the IP address is being used by other nodes

### DHCPOFFER
![CS3103-2-9.PNG]({{site.baseurl}}/img/CS3103-2-9.PNG)
- Broadcast: Nodes cannot participate if it does not have its IP layer configured (ipaddresa)
- Ip address
- How long use

### DHCPREQUEST
![CS3103-2-10.PNG]({{site.baseurl}}/img/CS3103-2-10.PNG)

> Question: Why is the request a broadcast?
	- To let the other DHCP servers know that the IP address is taken

### DHCPACK
![CS3103-2-11.PNG]({{site.baseurl}}/img/CS3103-2-11.PNG)

- Send 3 arp request to the same IP address
- This is to check if the IP address is being used
- Gratituous ARP

### DHCP renew before lease
![CS3103-2-12.PNG]({{site.baseurl}}/img/CS3103-2-12.PNG)


### DHCP release

![CS3103-2-13.PNG]({{site.baseurl}}/img/CS3103-2-13.PNG)

- When we shut down our laptop, not needing the ipaddress anymore


## Typical TCP/IP info

- Subnet 
- Netmask
- IP address 
- Router
- Domain
- DNS#1
- DNS#2

1. IPaddress
2. Default gateway
3. DNS server

> DHCP Discover and DCP request are broadcasted only on LAN/subnet. Does this mean we need one DHCP server for every IP subnet?
	- No, we use relay

## DHCP through Relay agent

![CS3103-2-14.PNG]({{site.baseurl}}/img/CS3103-2-14.PNG)


- Any dhcp comes, it will be relayed to the other
- Router here acts as the relay
- Router run both client and server program, listen on port 67 and intercepts any dhcp discover messages and forwards (unicast) the request to one or more DHCP servers.
	- Change router incoming IP address to its own in the router-address field
    - increments hop count to 1
- DHCP server recognises this request is coming from router and not client
	- Sends unicast reply to router
    - router replies to client
### Non-router
A relay agent can also be other nodes other than a router

![CS3103-2-16.PNG]({{site.baseurl}}/img/CS3103-2-16.PNG)

    
## Implementing multiple DHCP servers
![CS3103-2-15.PNG]({{site.baseurl}}/img/CS3103-2-15.PNG)

- Serves a specific network range
- this is for redundancy if there multiple


## DHCP Packet format
![CS3103-2-17.PNG]({{site.baseurl}}/img/CS3103-2-17.PNG)

- Hop count: Start from 0
- flags
- Gateway Ip address: for relay agent to put its ip address
