---
layout: post
published: false
title: 'CS3103 - Lecture 11: SDN (Software defined network)'
---
# Overview
SDN - Seperate control plane and data plane entities
- Network intelligence and state are logically centralise
- The underlying network infrastructure is abstracted from the applications

Openflow is communication interface/protocol between the control and data plane of an SDN architecture

- Network Virtualisation: Making a physical network appear as multiple logical ones (Network slicing)

### Why is it good
- Best effor packet delivery service
- Key functionalitu are programmable at the end hosts
- Ease of adding host and link tech
- Ease of adding sercvices
- Change is only easy at the edge

> There is nothing new at the core of the network

![CS3103-11-1.PNG]({{site.baseurl}}/img/CS3103-11-1.PNG)
- Hourglass IP model
- Layered service abstraction 
	- Decomposse delievery into fundamental components
    - Independent, compatible (Innovation at each layer)
- Only for network edges

## Current Internet: Complicate router at teh core
- Router can be partition into control and data plane
- Management plane: Configuration
- COntrol plane: Devision: Run routing algo/protocols (RIP, OSPF, BGP)
- Dataplane: Forwarding- forwarding datagrams from incoming to outgoing link

![CS3103-11-2.PNG]({{site.baseurl}}/img/CS3103-11-2.PNG)

### Dataplane
= Processing and delivery of packets
- Based on state in routers and endpoint
- E,g IP, TCP, Ethernet etc
- Fast timescles per packet

### Control plane
= Estanlishing the state in rrouters
- Determines how and where the packets are forwarded
- Routing, traffic engineering, firewall state
- Slow time scales(Per control event)

# What is wrong with the current internet
- Control by manufactors
![CS3103-11-3.PNG]({{site.baseurl}}/img/CS3103-11-3.PNG)

Application are like
- Routing
- Management
- Mobility management
- Access control
- VPN

- An industry with a mainframe mentaility
- Consequence: Buggy software in the equipment
	- Cascading failures, vulnerabilities, etc

### Operating a network is expensive
- More than half the cost of a network
- Yet operator error causes most outages

### Demand and complexity are increasing
- Major ISPs: Upgrade their internal network infrastructure (router and switches) every 18 months to keep up with the current demands for network

### other problems
- Close equipment 
	- Software bundle with hardware
    - Vendor-specific interfaces
- Over specified
	- Slow protocol standardization
- Few people can innovate
	- Equipment vendor write the code
    - Long delay to introduce new features
    
> Even if you standardised something, every vendor must agree to it. This would take some time because most vendors would not change it as they need to retest everything. Once somethig is deploy, it is very hard to change the software

# Networking as a discipline
- Other fields in the system: OS, DB, DS
  - Teach basic principles
  - Are easily managed
  - Continue to evolve
- Networking
	- Teach big bag of protocol
    - Notoriously difficult to manage
    - Evolves very slowly

> A failure from an academic point of view



