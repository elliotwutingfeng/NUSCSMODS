---
layout: post
published: true
title: 'CS3103 - Lecture 6 : Wireless Lan'
---
# MAC Sublayer - CSMA/CA
#### Characteristics


#### Standards



# MAC Sublayer = DCF and PCF
##### Recall: Eternet MAC layer (Listen while you talk)
- Send packet
- Listens
	- If detect collision:
    	- Jam channel
        - Back off
        - Wait
        - Attemp again, increase attempt counter
        - Discard packet
    - Else:
    	- Packet?

## MAC layer Protocol (CSMA/CA)
> What is the purpose of IFS
> 
> 
> What is the purpose of cotention window
>
> Then is collision avoidance achieved

### Why collision avoidance
- CSMA/CA looks more inefficient than CSMA/CD (Waiting times and ack)
- But we cant use CSMA/CD for wireless

> Why? (If cannot see each other, do they no its collision)
> 

### Collision detection is hard in wireless networks
- Enery level during transmission, idleness or collision
- Other requirements:


### Hidden node probelm
- CSMA/CA suffers from this
- Picture:


Station B and C are hidden from each other wrt A
-  B transmission to A may overlap with C transmission to A
- What happens while B is transmitting to A, C senses the carrier to start transmission?

> Hidden nodes reduce the capacity of the network as they increase the possibility of collision


#### MAC LAYER (CSMA/CA)


#### Reservation scheme (CTS) prevents hidden station problem



#### interframe space types (IFS)

Values:
- DIFS (Distributed coordination function IFS)
	- Longest IFS
    - Used as minimum delay of asynchronous frames contending for access
    - Used for all ordinary asyncronous traffic
- Short IFS (SIFS)
	- Shortest IFS
    - Ised for immediate response action. 
    - Pritority is given for response messsages over another new message from other stations
    - Clear to send (CTS)
    - Ack
    - Poll response
- Point coordination function IFS (PIFS)
	- Mid length IFS
    - USed by centralised controller in PCF scheme when using poll
    - Takes precedence over nomal contentin traffic

## Exposed node porblem

> What if C sends an RTS immediaately after timeout for CTS from B and no data in channel?


### RTS/CTS do not solve Exposed node problem
- C hears from RTS from A but not CTS from B
- After timeout period it sends RTS to D
- A is in sending state and not recieving
- D response with CTS
- Now C cannot hear D CTS because of collision
- C has to wait until A completes transmission


## MAC sublayer
- Two types of mac layer protocols:
	- DCF: Distributed coordination function
    	- Contention service (On top)
    - PCF: POlling service
    	- Optinal access method for infrastructure network
        - Used for time sensitive transmission

PCF is implemented on top of DCF


### PCF
- Provides a centralised contention free polling access method 
- PC (point coordinator) module at AP performs polling
	- Stations request AP register them on polling list
    - AP regularly polls stations on polling list and delivers traffix
- Both PCF and DCF operate simultaneously

How does PC (AP) gets access to media
- If 10 nodes are registered for polling and refrain from contention
- 4 nodes are not registered and operate in DCF mode 
- Hence AP will be contending with these 4 ndoes

Another IFS value is introduce PIFS. It is shorter than DIFS. AP use this to gain access to media
> How?


What happens if AP always uses PIFS?
> Startvation of DCF based stations


#### AP use reptition interval


# Lab Notes

## Basic service set (BSS) or cell
- Building Block of a wireless lan
- A set of station cotnrolled by a single coordiantion function, the logical function that determines when a station can transmit or recieve
- A BSS without an AP is called an ad hoc netowrk or IBSS (independent Basic service set)
- A BSS with an AP is called infrastructure network

## Extended service set (ESS)
- A set of one or more basic service set interconnected by a distributed system(DS)
- Traffic always flow via Access point
- DIameter of the cell is double the coverage distance between two wireless stations

### DS
- A system to interconnect a set of basic service sets
	- Intergrated (SIngle AP), Wired, Wireless

## SSID
- Service set identifier or Extended SSID
- Network name
- 32 octets long
- One network (ESS or IBSS) has one SSID

## BSSID
- Basic service set identifier
- cell identifier
- 6 octec long (mac address format)
- one bss has one BSSID
- Value of BSSID is the same as the MAC address of the radion in the access poinnt
- IN an IBSS, the BSSID is a locally adminsitered MAC address generated from a 48 bit random number

## Frame formats

## Field type desc

#### Why 4 adddresses




Questions:
- How a node associates with an AP
- How to handle mobility
- What are WEP and WPA2

    

# LAB
