---
layout: post
published: true
title: 'CS2105: Lecture 8 - Link Layer'
subtitle: Link Layer
---

## Introduction to link layer
- Network layer provides communcation service between any two hosts
- An Ip datagram may travel through multiple routers and links before it reach its destination

> The path go to multiple routers from path to server

- Link layer sends datagram between adjacent nodes (host or routers) over a single link
   - Ip datagrams are encapsulated in link layer frams for transmission
   - Different link layer protocols may be use on different links
> Different link protocols are use on different links

### Possible Link layer Services
- Framing
   - Encapsulate datagram into frame, adding header and trailer to the payload
   - This becomes a frame
   - Router will remove the header and trailer and add a new header and trailer
- Link access cotnrol
   - When multiple nodes share a same single link, need to coordinate which nodes can send frames ar a certain point of time.
- Reliable delivery
   - Seldom use on low bit error link(fiber)
- Error detection
	- signla faults
    - Signal noise
    - Depends on the link layer protocols
- Error correction
	- Receiver identifies and correct the bits
    
### Link Layer implementation
- Link layer is implemented in adapter or on chip
- Adapters are semi autonomous, implementing both link and physical layers

> Router only has up to 3 layers with the last layer being network, that is why router is consider a 3rd level device

- Transmission over the link is control by link layer protocol

## Error Detection and Correction
- Popular error detection
	- Checksum (TCP/UDP/IP)
    - Parity Checking
    - CRC (Link layer)
- It is not 100 percent relaible
	- May miss some errors but rare
    - Large error detection and correction fields yield better detection 
    
> CRC is slow if implemented in software thus it is better to be implemented in hardware not software 


### Parity Checks

#### Single bit parity
- Can detect single bit errors in data
- Select the parity bit such that the sum of the parity bit and the data is even
- e.g: if there are 9 ones in the data, we will choose a one in for parity bit so that it will be 10 in total (even)
- This only checks for one bit flip 
- Receiver will miss the error if two bits swap
- This is only use for reliable link transfer as it is fast
    
    
#### Two dimensional bit parity
- Can detect correct single bit errors in data
- Compute the sum for every row and every columnn and find the parity bit for each row and column where it must be even
- This can be use to detect exactly which bit is flip and correct it (oNLY IF ONE BIT)
> There is an higher overhead of bits that we need to sync (60 percent overhead). This is a tradeoff

#### Cyclic Redundancy Check (CRC)
- Powerful error detection coding that is widely use in practice
- D : Databits
- G: Generator of r + 1 bits agreed by sender and reciever
- R: Will generate CRC of r bits

- Calculation is done in bit-wise XOR operation without carry or borrow

e.g r = 3
![Capture.PNG]({{site.baseurl}}/img/Capture.PNG)

- Because r is 3, we will not remove the front 0
- Sender sends (D,R)
- Reciever knows G, divides (D,R) by G
	- if non 0 remainder: error is detected


## Multiple Access Links and Protocols

#### 2 types of network links
- Type 1: Point to point link
	- Sender and receiver connected by a dedicated link
    - Example protocols: Point to point protocol (PPP), Serial Line Internet Protocol (SLIP)

![Capture2.PNG]({{site.baseurl}}/img/Capture2.PNG)

- Type 2: BroadCast Link (Shared medium)
	- Multiple nodes connected to a shared broadcast
	- When node transmit a frame, the channel broadcast the frame and each other node receives a copy
    ![Capture3.PNG]({{site.baseurl}}/img/Capture3.PNG)

#### Multiple Access Protocols
In a broadcast cannel, if two or more nodes transmit at the same time
- Every node have mutliple frams at the same time
    - Cause collision
- Multiple access Protocol is used

Multiple access protocols can be categorized into 
- Channel partitioning
- Take turns
- Random access


### Channel partitionaing protocols

#### TDMA (Time division multiple access)

Time is divided into different slots
Each piece is further partition into slots
This pattern is repeated. Each nodes get a fix lenght slot
Unused slots go idle

- The first computer will get different slot
- Everyone willl get a few seconds to transmit
- This is similiar to CPU Scheduling > CS2106

#### FDMA (frequency division multiple access)
- Channel specturm divided into frequency bands
- Each node is assign a fixed band
- Unused transmission time in freq band go idel
- Every node is guranteed to use

> FDMA is used in radio signals where the receiver will filter and tune into that frequency and extract the band

### Taking Turns protocols

**Polling: Master node invites slave nodes to transmition in turn**
Every node has a chance to sent.

> We will not waste time to ask slaves that have no data to be transmitted. This is more efficient
#### Good
- Fair protocol
- Efficient compared to division

#### Bad
- There is an overhead for polling
- Single point of failure (Master node)



**Token passing: Control token is pass from one node to another sequentially**

It is only use for the token. Only the host with the token is allow to send data. Token is pass after one another. The nodes is usually organise in a ring.

#### Good
- No collisions

#### Bad
- Token overhead to pass
- Single point of failure (token)

### Random access protocols
When node has a packet to send
- A no priority coordination among nodes
- This might cause colllions (Two or most host are sending at the same time and it might collide)

RAP will specify:
- Detect collision
- Recover

#### Slotted ALOHA
Assumptions:
- All frames are of equal size
- Time is divided into slots of equal length (length = time to transmit 1 frame)
- Nodes starts to transmit only at the beginning of a slot

Operations:
- List to channel while transmitting (Detect)
- If collision: Node retransmits a frame in each subsequent slot with probability p until success
- p is design to respond to network congestion where a smaller p is chosen if there is a network congestion

![3 nodes sending at the same time]({{site.baseurl}}/img/Capture4.PNG)

### Good
- Simple to understand

### Bad
- Wasting some of the channel capacity
- Need synchronisation
- best case is 30 percent use of channel capacity

> If you have a large bandwidth, it is useless because we are only use 30 percent


#### Pure (Unslotted) ALOHA
Even simpler: No slots and no synchronisation

- When a node has a frame to send, it just transmit
- Chance of collision then increase:
	- Frame sent at t0 collides with other frames send in t0-1 and t0 +1

> The front frame may overlap with the next node

- Channel utitlization is worst here (15 percent)

#### Carrier Sense Multiple Access
CSMA sense the channel before transmission
- Idle: Transmit
- Busy: Defer transmission

> Human analogy: "Do not interrupt others"

*But will collision still happen?*
> Yes, if two nodes sense simultanously and found idle, they will transmit at the same time.

- Propagation delay: Two nodes may not hear each other transmission delay

When a node is at the far end of the transmission channel, that node may not know whether the other nodes is sending something.

> The protocol is not very smart, even thou there is a collision, it still continue to finish and retransmit

#### CSMA/DA (collision Detection)
Transmission is aborted quickly as soon as collision is detect
- Retransmit after a random amount of time

> This is the underlying method of ethernet

**Minimum Frame Size**
- What if the frame size is too small to be able to be detected that it collided
- This leads to no retransmssion
> This is why there is a certain limit to the frame size to ensure that CSMA/DA collision can be detected (Ethernet = 64 bytes min)

#### CSMA/CA (Collision Avoidance)
Collision detect is easy in wired LAN but difficult in wireless

A signal has a fixed range which can only be detected if within that range. Outside that range, it will become weaker.

![Hidden Node problem]({{site.baseurl}}/img/cap5.PNG)
The two laptop cannot detect each other thus it might collide

> 802.11 (WIFI) use CSMA/CS Protocol instead, receiver needs to return ACK if a frame is recieved OK.


## Switch Local Area Networks