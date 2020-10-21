---
layout: post
published: false
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

### Blue tooth communication process
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



# Slides
<iframe src="https://drive.google.com/file/d/1w-2Lrb6VESE1QaBbhJo8EbR14pht760D/preview" width="640" height="480"></iframe>
