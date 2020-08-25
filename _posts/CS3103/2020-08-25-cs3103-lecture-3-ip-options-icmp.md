---
layout: post
published: false
title: 'CS3103 - Lecture 3: IP - Options, ICMP'
---
# IP
![CS3103-3-1.PNG]({{site.baseurl}}/img/CS3103-3-1.PNG)

> Question: Why is there no Payload length?
> - total length - header length  can be use to figure out the payload length. The IP packet also might not alwyas be 20 bytes

The bits are transmissted row by row
- First transmit bits 0-7
- Then transmit 8-15
- then 16-23
- then 24-31

This is called network byte order or big endian byte ordering

> Note that many computers store 32 bit words in little endian format


#### Encapsulation of a small datagram in an ethernet frame

![CS3103-3-3.PNG]({{site.baseurl}}/img/CS3103-3-3.PNG)

The transmission shld be have a minimum length requirement so that we will be able to detect if there is a collision

#### Big datagram
![CS3103-3-2.PNG]({{site.baseurl}}/img/CS3103-3-2.PNG)

There is a need for maximum length requirement for ethernet due to avoiding corruption. Too big, if there is a corruption.. it will take v long to retransmit it.

## IP fragementation

![CS3103-3-4.PNG]({{site.baseurl}}/img/CS3103-3-4.PNG)

- Takes placde because of physical level limitation
- occurs at router or original sending host
- Reassembled at destination host

### Segmentation and Fragmentation

![CS3103-3-5.PNG]({{site.baseurl}}/img/CS3103-3-5.PNG)

TCP: 
- Divides them into segment base on the link layer 
- To avoid Fragmentation in the other layers

![CS3103-3-6.PNG]({{site.baseurl}}/img/CS3103-3-6.PNG)

UDP:
- There is no segmentation
- There is a max size 
- It goes to IP layer, and it will check the link layer to see if need to ip layer fragementation
- UDP header is only added to the first fragment


> Length of the data in each fragment must be in multiple 8 (except for the last packet)
> - 

# ICMP (IPV4)
