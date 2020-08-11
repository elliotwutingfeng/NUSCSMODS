---
layout: post
published: false
title: 'CS3103 - Lecture 1:  Introduction to subnet'
---
# Internet Today
![CS3103-1-1.PNG]({{site.baseurl}}/img/CS3103-1-1.PNG)

- IXP : Internet exchange provider
- PoP: Point of presence

# A simple TCP/IP Example
![CS3103-1-2.PNG]({{site.baseurl}}/img/CS3103-1-2.PNG)

The web client wants to access this web server through the web url.
> HTTP Client/server communication

![CS3103-1-3.PNG]({{site.baseurl}}/img/CS3103-1-3.PNG)

Http request:
![CS3103-1-4.PNG]({{site.baseurl}}/img/CS3103-1-4.PNG)

The web server will send a response with `200 OK`

To send the http, it needs to establish a tcp connection.

> Does the TCP work with hostnames? 
- Recall TCP Header, there is no place for hostname.. only for ipaddress and port number


The url is translated into a 32 bit ip address using a database lookup to a DNS Server.

![CS3103-1-5.PNG]({{site.baseurl}}/img/CS3103-1-5.PNG)

However, there is no mechanism for port number querying, but some port number are default. (e.g http = 80)

![CS3103-1-6.PNG]({{site.baseurl}}/img/CS3103-1-6.PNG)


### Invoking the IP protocol
- Send the datagram to the ip address
- Dtagram have the connection infomation
	- port
    - http
    - IP address
    
### Sending the ip datagram to an ip router
- Sometiems the clients are in different subnets
- It will only know if it is in the same network or not
- Send the IP datagrame to its default gateway (router)
- This gateway is configured when it is first set up (manually or through dhcp)

### Finding the MAC address of the gateway
This is for ethernet
- Translate the ip address to mac address
- ARP protocol
	- Does a broadcast
    - The intended recipient of the query shld reply their mac address
### Recieve at the router
- It wil send up the level until it reaches the application level
- Ethernet driver knows the content is an IP packet from the header (l2 frame header, ie Ethernet frame type)

- Sends the frame to the server using the mac address

### Data has arrived at server
- Payload of the IP datagram is passed to the IP protocol
- The payload of the IP datagrame is a TCP segment

> How does the ip module knows that the content is a tcp segment
- header protocol field 1byte


> Since the TCP segment is a connection request (SYN), the TCP protocol does not pass data to the http program for this packet. Instead the tcp protocol at neon will response with a syn segment to argon


### Conclusion
- The server only receive on packet {TCP-SYN}
- TCP connection takes up more work then the HTTP request
- Simplified
	- Transmission error
    - One router
    - Client knows how to connect to DNS


# Internet Address
- Each Ipaddress is a pair (Netid, hostid)

> How many bits for network and host
- Based on network mask
![CS3103-1-77.PNG]({{site.baseurl}}/img/CS3103-1-77.PNG)


## Special address
- First and last: Reserved and not assign
	- First: Netowrk indentification
    - last: Broadcast address
- Netowkr part all zeros: the host on this netowrks
- Host past all ones: Direct broadcast address

> The boradcast have limited else the whole internet would be flooded







