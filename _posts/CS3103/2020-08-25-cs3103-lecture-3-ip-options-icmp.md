---
layout: post
published: true
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

> Avoid fragmentation because if one fragment is corrupted, the entire thing must be retransmitted

![CS3103-3-6.PNG]({{site.baseurl}}/img/CS3103-3-6.PNG)

UDP:
- There is no segmentation
- There is a max size 
- It goes to IP layer, and it will check the link layer to see if need to ip layer fragementation
- UDP header is only added to the first fragment


> Length of the data in each fragment must be in multiple 8 (except for the last packet)
> - It is the size of a word

#### Question
1) If a packet has arrived with an M bit value of 2 and a fragmentation offset of 0. Is this first feag, last or middle?
> Middle, tseen through offset  = 0

2) A packet has arrived in which offset is 100, the value of Hlen is 5 and value of the total length field is 100. What is the number of first byte and last byte of the IP payload

>  Start: 8*100
> Offset : 100 - 20 = 80 [Total length - Header size]
> End bit: 800 + 80 -1 = 879 (start from 0)


# ICMP (IPV4)
