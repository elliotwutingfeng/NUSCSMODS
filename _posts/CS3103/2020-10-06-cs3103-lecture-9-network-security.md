---
layout: post
published: false
title: 'CS3103 - Lecture 9: Network Security'
---
# Link state routing
Each router in the network knows the link state so that they can plan the appropriate path
- Distance vector: Router knows only cost to each destination
- Link state: Router knows the entire network topologu
	- Computes shortest path by itself
    - Independent computation of routes
    
![CS3103-8-1.PNG]({{site.baseurl}}/img/CS3103-8-1.PNG)

#### Forming shortest path tree for router A in a graph (Dik Algo)
![CS3103-8-2.PNG]({{site.baseurl}}/img/CS3103-8-2.PNG)
![CS3103-8-3.PNG]({{site.baseurl}}/img/CS3103-8-3.PNG)

THe cost can be anything depending on the protcol (like latency)

Reading the table:
![CS3103-8-4.PNG]({{site.baseurl}}/img/CS3103-8-4.PNG)


# OSPF
The open shortest path first protocol is an intradomain routing protocol based on link state routing. Its domain is also an Autonomous system

Key elements:
- Topology dissemination
- Usses link state routing to compute shortest routes

- Open pub available
- Uses link state algo
	- LSA dissemination
    - Topology map at each node
    - route computation using dikjstra algo
- LSA flood throughout the entire AS
	- Does not use any transport layer
    - Directly over IP (Not UDP OR TCP)

Area in autonomus system
 ![CS3103-8-5.PNG]({{site.baseurl}}/img/CS3103-8-5.PNG)

- Within an OSPF area, all router maintain the same topoly database. They have no knowledge of netowrk topolgies outside the area
- There is always one router connected to the outside
- There is two types of router
	- Area border router: Lets network knows about the outside
    - Backbone router
    - AS boundary router: Carry infopmation of the network and send outside
    

![CS3103-8-6.PNG]({{site.baseurl}}/img/CS3103-8-6.PNG)

# Types of Links
- Point to point
- Transient
- Stub
- Virtual

## Point to point

![CS3103-8-7.PNG]({{site.baseurl}}/img/CS3103-8-7.PNG)


- Connect router direct (The two router must be connected to each other)
- Can be backbone
- Can be for any area

Any arisement come to the network or from, it is applicable for both router


## Transient

![CS3103-8-8.PNG]({{site.baseurl}}/img/CS3103-8-8.PNG)


- Network have multiple router
- Packet enter and leave through any rotuer

### Designated Router (DR)
Our network sending infomation to the router but the subnet cannot speak for itself. For a broadcast domain with N router, its LSA Message complexity could be O(n^2)

- Designated router and backup router are elected to represent the subnet and broadcast subnet info (Using HEllo protocol)
- All advisement/info will be done by designation router
- ANy router that find changes, will communicate to DR
- DR will broadcast to everyone
- Backup will take over if the DR is not operating
- Each router will only have DR and BDR as neighbour


![CS3103-8-9.PNG]({{site.baseurl}}/img/CS3103-8-9.PNG)




