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


