---
layout: post
published: false
title: 'CS3235 - Lecture 2 : Network Attacks'
---
# Threat Model
-  Desired Security property/ Goal
- Attacker capabilities
- Assumption about the setup

![CS3235-2-1.PNG]({{site.baseurl}}/img/CS3235-2-1.PNG)

# How the internet works
- Collection of subnetworks
- Each sits on ISP (Autonoumous system)


#### ISP
- Special router
- Runs on BGP

> What is the outgoing link to move packet

![CS3235-2-2.PNG]({{site.baseurl}}/img/CS3235-2-2.PNG)

# BGP (TCP/IP: Physical layer)
- NLRI Update: Network Layer reachability infoamtion

Announce to the world that it knows the gateway info. The info will then propagate from AS to AS

## Route Hijacking
- Send false info about routes
- Swamp the BGP link & force traffic
- Readvertise withdrawn routes
![CS3235-2-4.PNG]({{site.baseurl}}/img/CS3235-2-4.PNG)


![CS3235-2-3.PNG]({{site.baseurl}}/img/CS3235-2-3.PNG)

# IP (Physical: Network layer)
- UDP: Unreliable
- TCP: Reliable - Ensures that the packet reaches




# Slide
<iframe src="https://drive.google.com/file/d/1BJTghBVw-hTH2GbZPdkzM8dbWUva0dMb/preview" width="640" height="480"></iframe>