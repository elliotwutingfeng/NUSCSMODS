---
layout: post
published: false
title: 'CS3103 - Experiment 8: IPSEC'
---
# Foruzan

![CS3237-lab-8-1.PNG]({{site.baseurl}}/img/CS3237-lab-8-1.PNG)
- IPsec in transport mode does not protoect the IP header
- Only protects the packet from the transport layer (Payload)
> This is due to the IPsec Header added to the info comig from the transport layer

- Transport mode is normally use when need end to end protection of data
- The receiving host uses IPsec to check the authentication and or decrypt the IP packet and deliever it to the transport layer

![CS3237-lab-8-2.PNG]({{site.baseurl}}/img/CS3237-lab-8-2.PNG)

# Tunnel mode
- Protects the entire IP packet
- Takes IP packet and applies IPsec seciryity method to the entire packet and then addes a new IP header 
![CS3237-lab-8-3.PNG]({{site.baseurl}}/img/CS3237-lab-8-3.PNG)


