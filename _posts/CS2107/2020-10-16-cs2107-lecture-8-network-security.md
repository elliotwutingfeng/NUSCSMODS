---
layout: post
published: false
title: 'CS2107 - Lecture 8: Network Security'
---
# Network layers

- Partions a complex communcation system into several abstraction layers
- The peer entities at the same layer N communcate with each other by executing a protocol at that layer


## Why
- Layer N protocol is built on top of virtual connection at layer N-1 below
- Example of protocol at layer 5 (Authentication protocol):
	- A -> B "Hello"
    - A <- B: certificate of B

- The virtual connection at layer 4 sends the message "hello" from A to B in step 1 and sends B certificate in step2

- At layer N:
	- A message to be send is called layer N protocol data unit (PDU)
	- Encapsulation of upper layer PDU

## Security weakness
- Original network design does not account for intentional attacks
- Possible threats:
	- Interception: unauthorised viewing
    - Modification: Unauthorise change
    - Fabrication: Unauthorised creation
    - Interruption: Preventing authorized access
- An attacker at any layer can modify the data and the header:
	- Consider the source IP address in the IP header
    - Wihtout protoection, the attack can send a packet with spoof source ip address
    

# Name resolution and attacks

- Each peer entity has a name
- on a single node at different layer, the name can be different

## Naming schemes and resolution
- Peer entity use virtual connection in layer below to find the corresponding name mapping
- E.g ip address of domain name
- Protocols that perform name mappings are resolution protocols
- Many resolution protocol didnt take into account of security, attackers can manipulate the outcome


## Resolution protocols
- DNS (Domain name system)
	- Maps domain name to IP address
    - Hierarchical decentralised naming system
    - Attacker can target the association of domain name with IP address
- ARP (ADdress resolution protocol)
	- Associates or Maps ip address (Logical) with Mac address (physical)
    - Use broadvase mechanism in local
    - Attacker on local can target the association
    
## DNS
- Ipaddress found by looking up a locally stored hash table or querying a dns server
- This is called name resolution
- Entity (Client) that initiates is called resolver
- If a domain name is found, this is called resolved

### Light weight authentication of DNS query
- Query comes with 16 bit number (QID): Query ID
- Response must also come with QID
- IF QID in response does not match the one in the query, the client rejects the answer
- No encryption or MAC is used

> QID was originally not meant for authentication but efficient way to match multiple queries

### Local DNS Attack

ALice:
- Use free wifi to surf
- wants visit a page something.com
- types domain name into browsers address bar

ALice browser:
- Makes query to DNS server to determin the IP address
- connects to IP address after obtaining it

Mallaory (attacker)
- At physical layer: Can be another person in the same wifi
- WIFI is not protoected so attacker can:
	- Sniff data from communciation channel
    - Spoof data from the communication channel
- AAttacker cannot remove/modify data already sent by ALice
- Attacker owns a web server with IP address that is a spoofed something.com website


#### Attack
1. Alice ask for address
2. Mallory sniff and knows abt it
3. She spoof a reply with the same QID
4. DNS server also sends a reply
	- Since Mallory is closer to ALice
    - Mallory reply is likely reach Alice first
5. Alice takes first reply as answr and connect to spoof website

#### Additional remarks
- DNS is at application layer
- Attacker at physical layer and is just below the application layer: There exist some virtual connection that can send the message across
- DNS is important component as it resovles the domain name
- DNS can be a single point of failure for network
- DoS instead of attacking webserver could attack the DNS server instead


# Denial of services attacks



# Userful network security tools
# Protection: Securing the communication channel using cryptography
# Protection: Firewall
# Protection: Network security management