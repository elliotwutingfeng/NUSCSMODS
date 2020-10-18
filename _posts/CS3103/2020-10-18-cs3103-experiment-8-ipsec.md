---
layout: post
published: true
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

## Tunnel mode
- Protects the entire IP packet
- Takes IP packet and applies IPsec seciryity method to the entire packet and then addes a new IP header 
![CS3237-lab-8-3.PNG]({{site.baseurl}}/img/CS3237-lab-8-3.PNG)

Tunnel mode:
![CS3237-lab-8-4.PNG]({{site.baseurl}}/img/CS3237-lab-8-4.PNG)


> The tunnel mode protoects the original IP header

In tunnel mode, the flow is from the network layer to the IPsec layer and then back to the network layer again


![CS3237-lab-8-5.PNG]({{site.baseurl}}/img/CS3237-lab-8-5.PNG)

## Two security protocol
- AH
- ESP
Provide authenticaiton and or encryption for packets at the IP level

### Authentication header (AH)
- Authentication the source host
- Ensure the integrity of the payload in IP pakcet
- Hash function and sym secret key
- Digest inserted in the authenticaion layer


1. Authentication header is added to payload with data field being 0
2. Padding may be added to make total length even
3. Hawshing is based on total packet
4. Auth data are inserted in the authentication header
5. IP header is added after changing the value of ht eprotocl field to 51

![CS3237-lab-8-6.PNG]({{site.baseurl}}/img/CS3237-lab-8-6.PNG)

Fields:
- Next header: Defines type of payload
- Payload length: Does not define length of payload but the length of the authenticaion layer in 4 byte multiples and does not include the 8 byte
- Security para index: (32 bit) Pays the role of virtual cirvuit identifier and is the same for all packets sent during a connection call security association
- Sequence number (32 bit sequence number) provides ordering info for a sequence of datagrams. Prevents a playback.  A new connection must be establish if the seq num reach max 2^32
- Auth data: Result of applying hash function to entire IP datagram except for fields that changes during transit like time to live

### Encapsulating security protocol
- AH only Provides source auth and data integrity but not confidentiality
- ESP provides auth, integrity and confidentiality
- Adds header and trailer
- Auth data add at end of packet so its cal is easier
- Value of protocol field in IP header is 50

1. Esp trailer add to payload
2. Payload and trailer are encr
3. The ESP header added
4. The ESP header payload and ESP trailer are use to create auth data
5. The auth data are added to end of ESP trailer
6. The Ip header is added after changing protocl value to 50

![CS3237-lab-8-7.PNG]({{site.baseurl}}/img/CS3237-lab-8-7.PNG)

Fields:
- Security para index: (32 bit) similiar to AH
- Sequence: SImiliar to ah
- Padding : 0s 
- Pad length: (8 bit) defines the number of padding bytes/ The value is between 0 and 255
- Next header: (8bit) same as AH
- AUth data: Applying an auth scheme to parts of the datagram. The difference is Ah( Part of the IP header is included in calculation of auth data while ESP is not)

### AH vs ESP
- ESP is better that AH
- We dont need AH
- AH are still part of the internet

### Services by IPSec
![CS3237-lab-8-8.PNG]({{site.baseurl}}/img/CS3237-lab-8-8.PNG)

- Access control: SAD (Security assicaion database) ensures that the packet is discarded if there is no security assication establish for that packet
- Message integrity: Preserve in both AH and ESP. The digest of data is created and sent by sender to be checked by receiver
- Entity auth: The security association and key hashed digest of the data sents by the sender auth the sender of the data in both AH and ESP
- Confidentialtiy: Encryp of message in ESP provides this but not for AH. 
- Replay attack protection: Both is prevented using seq number and sliding receiver window. Each IPSEC header contains a unique seq number when the security association is established. The number start from 0 and incraeases until the value reaches 2^32 - 1. When the seq number reaches max, it is reset to 0 and at the same time the old security assocation is deleted and a new one is establish. To prevent processing of dups: IP mandates fix size window at reciever.

### Security Assicoation
- Contract between two party
- Create secure channel\
- Provides integrity and authentication for message

### SAD 
- Database
- Define a single SA
- Two SAD: inbound and outbound
- Host need find corresponding entry in the outbound SAD to find the infomation for applying security to the packet
- Receiving host needs to be sure that the correct info is used for processing the packet

### Security policy
- Defines the type of security applied to a packet when it is to be sent or when it has arrived
- Host mus determine the predefine policy for the packet

### Security policy Database
- Each host keeps SPD
- Sextuple index:
	- Source address
    - Dest address
    - Name
    - Protocl
    - Source port
    - Destination port
- Source and dest address can be unicaast mult or wild card
- Name defines DNS entity usually
- Protocol eithe AH or ESP
- SOurce and dest port are for the process running at source and dest

#### Outbound
- Sent out, consult this SPD
- Input is sextuple index
- Output:
	- Drop: dont sent
    - Bypass: No need header
    - Apply: Apply security according to SAD, if dun have create one
![CS3237-lab-8-9.PNG]({{site.baseurl}}/img/CS3237-lab-8-9.PNG)

#### Inbound
- Arrives
- Entry access using sectuple index
- Output:
	- Discard: Drop the packet
    - Bypass: No need header
    - Apply: Base on SAD
    
![CS3237-lab-8-10.PNG]({{site.baseurl}}/img/CS3237-lab-8-10.PNG)

### IKE Internet key exchange
- Protocol
- Create both inbound and outbound
- IKE is online
- Based on
	- Oakley: Key creation 
    - SKEME: Key exchange (PKC)
	- ISAKMP: Implements the exchanges define in IKE
    
## VPN
- Private but virtual
- Guarantees privacy inside the org
- Virtual cos it doesnt use real private WAN
- Network is physically private but virtually private
- VPN uses ESP protocol of IPsec in tunnel mode
- Private datagrame incl the header is encap in ESP packet
- Router at border uses its own ip addrtess and add of arouter at the dest site in new datagram
- Decipherings takes place at R2

![CS3237-lab-8-11.PNG]({{site.baseurl}}/img/CS3237-lab-8-11.PNG)

