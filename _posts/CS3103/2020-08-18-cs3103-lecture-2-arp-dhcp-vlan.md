---
layout: post
published: false
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

Arp cache contains address mapping for all host within a single LAN

## ARP Packet Format


