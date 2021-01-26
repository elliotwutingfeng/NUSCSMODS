---
layout: post
published: true
title: 'CS3235 - Lecture 3: Secure Channels'
---
# Introduction to secure channels

- Assumption
- Prove based on the assumption
- Do not make too much additional assumption while proving

#### Definition
1. Define adversary
2. Define goal/ Security property

![CS3235-3-1.PNG]({{site.baseurl}}/img/CS3235-3-1.PNG)

#### Examples
- SSH
	- Connect SSH client to ssh server
    - Secure channel
    - Replace telnet
    - Integrity/ Confidentiality
- MIM 
- Encryption prevent Evesdrops
- Digital Certs (SSL certs)
- HTTPS: TLS or SSL

# Types of adversary
- Cipher Only Attacker
	- Only knows ciphertext
    - Tries to get plain text
- Known Plaintext Attack
	- Give ciphertext for some plaintext
- Chosen Plaintext attack
	- See ciphertext for chosen set of plaintext
    - Asked to guess for the decryption for unknown ciphertext
    - Get decryption method
- Chosen Ciphertext attacker
	- Get plaintext
    - See Decryption of cipher
    - guess plaintext

# OTP (one time pad)

Encryption

Definition: 
- Getting cipher text c does not reveal anything about what we already know about M
	- length 
- Probability must be the same for all encruption, that measn, given a ciphertext, the probability of it being M1 and M2 is the same

Problem:
- Shannon result: States that the key size must be greater than or equal to msg size
- This is bad because it means we need longer keys for big files

# Relax definition of secrecy
- The real adversary is efficient and has limited computational power
- Can execute in polynomial amt of steps
- Had randomised and non determinstic execution


# Symmetric key cryptosystem

Confidentiality and intergrity


- Block, stream ciphers [Confidentiality]
- MAC (Message authentication code) [Integrity]

Blocks:
- Stream cipher / PRG (Psudorandom generators)
- Cryptograph hash functions
- Block ciphers/ Pseudorandom permutation (PRPs)



# Slides
<iframe src="https://drive.google.com/file/d/1umJw-6DuqqNLYDw7iIsaoR5f5d8k29Cu/preview" width="640" height="480"></iframe>
