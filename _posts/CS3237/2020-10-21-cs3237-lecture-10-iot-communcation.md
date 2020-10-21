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

# Slides
<iframe src="https://drive.google.com/file/d/1w-2Lrb6VESE1QaBbhJo8EbR14pht760D/preview" width="640" height="480"></iframe>
