---
layout: post
published: false
title: 'CS2107 - Lecture 5 : Data Origin, MAC and signature'
---
Authentication: The process of assuring that the communicating entity or the origin of piece of infomation is one that it claims to be

Two types:
- Entitiy authentication
	- For connection oriented communication
    - Communicating entity is an entiryt involved in a connection
    - Mechanism: Password, challenge and response, biometrics
- Data origin authentication
	- connectionless communication
    - Communicating entity is the origin of a piece of infomation
    - Data origin authenticity implies data integrity
    - Mechanism: MAC or digital signature

![CS2107-4-1.PNG]({{site.baseurl}}/img/CS2107-4-1.PNG)


# Crypto background: Public key cryptography

##### Symmetrical
A symmetrical key encryption scheme use the same key for both encryption and decryption

![CS2107-4-2.PNG]({{site.baseurl}}/img/CS2107-4-2.PNG)

##### Public key scheme:
A public key (Asymmetric key) scheme uses two different keys for encryption and decryption
![CS2107-4-3.PNG]({{site.baseurl}}/img/CS2107-4-3.PNG)

- The two key must be related in someway even tho they are not the same


- Typical use: Owner keep private key secret but tells everyone her public key
- Suppose someone has a plaintext x for the owner, the person can encrypt it using the public key and post the cipher text to the owner
- ANother person cannot derive the plaintext without the private key even thou they have the public key

![CS2107-4-4.PNG]({{site.baseurl}}/img/CS2107-4-4.PNG)

- G - Generates a key pair, publicj and private
- E - Encryption algo
- D - Decryption algo


Requirements:
- Correctness
- Efficientcy: Fast, polynomial tie
- Security: "one way" function, the E() can be efficiently done but its inverse D() is infeasible without the private key (kd)


Trapdoor function:
- It inverse can be efficiently evaluated with the trap door kd
- Without the kd, there is a asymmetric computational requirenment between E and its inverse D

Security requirement:
- Difficult to determine plaintext without the private kkey
- **Implies** Difficult to get the private key from the public key

> See the tut 4 why cant we require that it must be difficult to get the private key from publick key


##### Suppse key scheme and advantages in Key management
- Suppose we have n entities
	- Each of them can compute a pair of public and private key
    - Each announces his public key but keep private key secret
- Suppose A wants to encrypt m for B
	- Use A public key to encrypt  m
    - By property of PKC only A can decrypt
- If we use SKC


## RSA
## Security of RSA
## Improper RSA usage

# Crypto background 2: Hash and keyed-hash
## Hash 
## Keyed hash


# Data integrity

# Data Authenticity (Mac, signature)
## MAC
## Signature

# Some attacks and pitfalls
## Birthday attack on hash
## Use encryption for authenticity
# Application of hash: Password file protection 
