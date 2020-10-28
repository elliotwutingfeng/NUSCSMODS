---
layout: post
published: true
title: 'CS3237 - Lecture 10 : IOT Communcation'
---
![CS3237-10-1.PNG]({{site.baseurl}}/img/CS3237-10-1.PNG)

# Wireless communcation

![CS3237-10-2.PNG]({{site.baseurl}}/img/CS3237-10-2.PNG)

- WPAN: Wireless Personal area
- WLAN: Wireless local area
- WMAN: Wireless metropolitan - For the city
- WWAN: WIreless Wide area network 

> The difference is the range

## WPAN
- Reaches varies from a few centimeters to a few meters

There are two classes:
- IP based
- Non IP bassed

## Non ip based WPAN
- Bluetooth: Wireless technology standard for exchanging data between fixed and mobile devices over short distances using short wavelength ultra high frequenct radio waves in the ISM bands
- ZigBee: Specification for a suite of high level communcation protocols used to create WPAN with small, low poer digital radios. Zigbee is a low power, low data rate and close proximity wireless ad hoc network using ism 2.4 ghx in most places


Bluetooth:
- Low power wireless connectivity technology
- Ultra low power bluetooth

## Blue tooth communication process
- Comprised of two wireless tech systerm:
	- Basic rate
    - Low energy
- Nodes can be either advertisers or scanner
	- Advertisers: Devices transmitting advertiser packets
    - Scanners: Device Receiving advertiser packet without the intention to connect
    - Initiators: Devices attempting to form a connection
![CS3237-10-3.PNG]({{site.baseurl}}/img/CS3237-10-3.PNG)

> 
> - advertiser sends advertisements.
> - scanner receives advertisements.
> - initiators connect in response to a scanned advertisement.


> Wireless headphoen advertise, iphone is initiator to connect to that advertisment

### Events
- Advertisments: Broadcast to scanning devices altering them of the wish to either pair or relay a message in the advertisment packet
- COnnecting: Process of pairing device and hsot
- Peridoic scanning

### Process
1. Advertise issues connectable agent
2. Listern can become initiator by making connection request
3. Advertiser determins if its wishes to form connection
4. COnnection is form the advertising event ends
5. Init called master
6. Advertiser is now call slave
7. The connection is termed a piconet

### BLE connection
![CS3237-10-4.PNG]({{site.baseurl}}/img/CS3237-10-4.PNG)

State:
- Initiating 
- Connected
- Standby

![CS3237-10-5.PNG]({{site.baseurl}}/img/CS3237-10-5.PNG)

### BLE Profile - Generic access profile (GAP)
- Controls connection and advertising in bluetooth
- Device roles: Peripheral IOT Device and Centrea
- Advertise data
	- Peripheral wants to send data to more than one device to a time 

### BLE Profile: Generic Attribute Profile (GATT) 
- Defines the way that two BLE devices transfer data back and forth using concepts using Services and characteristics
- Makes use of a generic data protocol: Attribute protocol (ATT)
- ATT is used to store services, characteristics and related data in a simple lokuptable using 16 bit ID for each retry
- GATT comes into play once the connection has been established

### Server-client relationship
- Peripheral is the GATT Server that holds ATT lookup data, services and characteristics
- Phone is the GATT client that sends request to the server


### GATT
- Transaction are started by client who gets response by server
- periphareal suggest a connection interval to the device during connection

![CS3237-10-6.PNG]({{site.baseurl}}/img/CS3237-10-6.PNG)

#### Services
- USe to break data up
- Service can have more than one characteristics
- Each service have a unique numeric ID called a UUID

#### Characteristics
- Encapsulate a single data point
- Each characterics has a predefined 16bit or 128 but UUID
- Characteriics can read write notifry property

	- Read: Central reads a data from a peripheral chara
    - Notify: Peripheral infoms central device that a new data value is available in a specific chara
    - Write: central writes a data in a peripheral chara

#### Transaction property
- Read property: Read the temperature
- Write property: How to react to the change
- Notify property: Notify the change

## Zigbee
- WPAN protocol based on IEEE 802.15.4 foundation targeted for commercial and residential IoT networking that is constrained by cost, power and space
- Low power wireless mesg networking


### Components
- Single ZC
- ZC can behave like ZR after connecting

#### ZR (Zigbee router)
- Not necessarily needed
- Optional
- Handles some load of mesh

#### ZED (Zigbee end devices)
- End point device
- Can communcicate with router or controller
- Cannout route
- e.g light switch, thermostate

### Data traffic
- Periodic data: Delievered at a rate defined by application
	- Sensor preiodically transmitting
- Intermeittent data: Application or external stimulus occurs at random rate
	- light switch
- Repetitive low latency data: Allocate time slots
	- computer mouse or keyboard
    
    
### Topo
![CS3237-10-7.PNG]({{site.baseurl}}/img/CS3237-10-7.PNG)

# Benefits of IP
- Ubiquity
	- IP stacks are provided by nearly every operating system and every medium
    - IP specifies the exact format for all data communications and the rules used to communicate, acknowldege
- Standard basded
- Scability
	- IP has demostrated scale and adoption
    - IPV6 could provided a unique IP address to every atom 
- Reliable
	- Assumes data is not guaranteed to be delivered
    - Packet is treated as independent
    - IP is connectionless because each packet is treated independently
    - IP is best effort delivery

## IP based WPAN
- Low power RF communcation system doest not need high bandidth
- Simplest of sensor can act as network citizen

### 6LoWPan TOPO
- Similiar to zigbee
- Mesh netowkrs residing on the periphery of larger networks 
- Topo are flexible
- Can be connected to the backbone or internet using edge routers

### Nodes movement
- Nodes are free to move and reorganised/reassembled in a mesg
- A node can move and associate with a different age router in a multi home scenario or even move between different 6lowWan meshes

## WAN
- Long range communication
- Connects the local network containing the IoT devices to the internet
- Long range communciation is usually a service, it has a subscription to a carrier providing cellular tower and infrastructure improvements


### Cellular connectivity
- Seperation of frequencies from neighbours neartest
- honey comb structure: Make sure that each of the frquency cannot interfere with the other holes
- No two similiar frquencies are within one hex space from each other
- But there is possible to have intererences in hex spaces with different colour

![CS3237-10-8.PNG]({{site.baseurl}}/img/CS3237-10-8.PNG)


# Connectivity of IOt Devices to internet
- Different from consumer based cellular devices
- Smartphone pulls info off internet
- IOT, data can be sparse and arrive in burst
- Maj of adata is generated by tge devices and travel over iplink

# Slides
<iframe src="https://drive.google.com/file/d/1w-2Lrb6VESE1QaBbhJo8EbR14pht760D/preview" width="640" height="480"></iframe>
