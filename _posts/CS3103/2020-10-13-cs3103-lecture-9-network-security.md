---
layout: post
published: false
title: 'CS3103 - Lecture 9: Network Security'
---
# Attacks on internet

Threats:
- Disruption: From an over reliance on fragile connectivity
	- Premeditated internet outrages bring trade to its knees
    - Randsomware hijacks the itnernet of things
    - Priviledge insiders coerced into giving up their crown jewels
- Distortion: As trust in the integrity of infomation is lost
	- Automated misinfomation gains isntant credibility
    - Falsifed infomation compromises performance
    - Subverted blockchains shatter trust
- Deterioration: When controls are eroded by regulations and technology
	- Surveillance laws expose corporate secrets
    - Privacy regulation impede the monitoring of insider threats
    - A headlong rush to deploy AI leads to unexpected outcomes


Original vision: A group of mutaully trusting users attached to a transparent network
- Infecting/attacking host/ users: Malware, spyware, spam emails, phishing, unauthorise access
- Denail of service: Deny access to resources
- Network of compromised devices/nodes is known as botnet
     - Control by bad guys
     - Use for spam email, distributed DoS

## Malware
- Virus: Infection by receiving object
- Trojan Horse: Hidden parts of some otherwise useful software
- Worm:  Infection by passively recieving (It gets executed itself)
- Spyware: Infection by downloading webpage with spyware
	- Records keystrokes, websites visited and upload infomation into collection site

> Worm and virus is self replicating: Propogates itself to other hsots and users

Ransomware: Is a type of malware/crimeware that encrypt a user's data then demands payment in exchange for unlocking the data



## Denial of service
- Attackers make resources unavailable to legitimate traffix by overwhelming resource with bogus traffic
	- Select target
    - Break into host around network
    - Send packet towards target from compormised host (TCP SYN packets)


## Intude
- Sniff, Modify, Delete your packets
- IP spoofing: Send packet with false source
- Record and playback: Sniff sensitive info and use later


Cheat:
- Phishing: Web/UR: phishing email phishing
![CS3103-9-1.PNG]({{site.baseurl}}/img/CS3103-9-1.PNG)

# Services by security system

