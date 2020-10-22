---
layout: post
published: false
title: 'CS2107 - Lecture 7: Access control'
---
# Overview of layering model in conmputer design
#### Layers in computer system


#### Comparing to layers in communication network
Network:
- The boundary is more well defined
- Infomation/data flows from the topmost layer down to the lowest layer and is transmited from the lowest layer to the topmost layer
- A concern of data confidentiality and integrity

Computer system:
- The boundary is less well defined
- Every layer has its own "processes" and "data" (although ultimately, the raw processes/data are handled by hardware)
- The main security concern is about access to the process and memory storage
- Hence beside data confidentiality and integrity (E.g password file), there is also a concern of process "integrity" whether it deviates from its original path

#### Attackers and system's layer
- Suppose an attacker sneaks into layer 1
- The attacker must not be able to directly manipulating object/data and processes in more priviledge Layer 0
- Note that is is very difficult to ensure this requirement

## Security Mechanism
- It insightful to figure out at what layer a security mechanism/attack resides
- A lyer based security mechanism should have a well defined security perimeter/boundary


- Important design consideration:
	- How to prevent attacker from getting access to a layer inside the boundary
    - E.g: SQL injection attacks target at the SQL DBMS.
    - The OS password management: Remain intact even if SQL injection attack
- Possible application takes care of its own security (Self-secure):
	- E.g application always encrypt its data before writing them to file system
    - Even if access control of the files system is compromised (e.g malicious user can read someone else files), the confidentiality of the data will still be preserved

# Access control model


# Access control in UNIX/Linux
# UNIX/Linux: Elevated privilged

