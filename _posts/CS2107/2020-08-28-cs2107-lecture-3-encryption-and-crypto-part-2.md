---
layout: post
published: true
title: 'CS2107 - Lecture 3: Encryption and Crypto part 2'
subtitle: Continue from lecture 2
---
#### Useful Heuritics
- SIngle letter:
	- a -  an indefinite article
    - iL the first (singular) person
- Diagraphs: to, it, is , do , on, in, at, of, or, an, he...
- Trigraphs: the, and, for, had, one

Commonly used letters:
![CS2107-2-1.PNG]({{site.baseurl}}/img/CS2107-2-1.PNG)

### Security of vigenere cipher	
- Vinener cipher is an improvement over shift
- Different occurance of same letter have differnet mapp letters
> Is it secure agaisnt known plaintext attack? 
> 	- NO


> Is it secure agaisnt cipher only attack?
> - Need a good attack technique

Suppose we know k = length/period of the keyword

Observation: all letters of the plaintext whose index is i(mod k) for i =0 to k-1, get shifted by the same key character

**In conclusion: Vigenere cipher turns into a monoalphabetic cipher again**


### Security Guarantee: Perfect secrecy
- "Regardless of any prior info that the attackers has about plaintext, the cipher text shld leak no additional info about the plaintext"
- can be defined in terms of conditional probabiltiy: 
	- P[M=m]: Attacker prior knowledge of unknwon plaintext m
	- P[M=m given C =c]: Attacker updated knowledge of the unknown plaintext m after the attacker has seen the ciphetext x
![CS2107-2-2.PNG]({{site.baseurl}}/img/CS2107-2-2.PNG)

> For AES, just need to stuff the title into AES Scheme and match the corresponding cryptotext

Issue: The key must be at least as long as the message itself

> - Is it unnecessarily strong for practical usage
> - Any security notoion that is more relax and practical

#### Substitition cipher Questions
- Key space: Set of possible keys
- Key space size: total number of possible keys
- Key size of key length: the number of bits required to represent a particular key


**Why is log2(27!) the lower bound of key size / length**
> - Possible Key representation:
>	- 1 byte per symbole: 27*1 byte = 27 bytes = 216 bits
> 	- 5 bits per sumbol/character: 27*5bits = 135 bita

Consider alice and bob, they are honest parties. We have 27! possible keys. Lets assume both alice and bob can manage to keep a key table where we have a list of exhastive list of keys in the same order. Given index, some how alice and bob can generate the key representation.
- How many entries: 27!
- We just need to encode the index: one index is just log2(27!)


# Modern Ciphers: Block Ciphers

![CS2107-2-3.PNG]({{site.baseurl}}/img/CS2107-2-3.PNG)
![CS2107-2-4.PNG]({{site.baseurl}}/img/CS2107-2-4.PNG)


Block cipher is an important cyrpto primitive: used in several schemes
Example block ciphers:
- DES: n - 64 bits, s = 56 bits
- 3DES: n - 64 bits, s = up to 168 bits
- AES: n = 128 bits, s = 128, 192, 256 bits

> For AES shld be at least 128


The longer the key is:
- More secure
- Slower

> See tut 2 for possible attack


## Block cipher - definition
Requirements:
- G( Key gen algo) that generates k
- Need to abstract what a block cipher really does: A math model of a block cipher
- Keyed PRP (Pseudorandom permutation): E: K.X -> X
	- There exist an efficient deterministic algo to eval E(k,x)
    - The output **looks random** such that it is indistinguisable from random function
    - The function E is **bijective (1-to-1)**, and thus is **length preserving**
- There exist an **efficient** inversion D(k,y), which thus satisfies the correctness requirement: for all m in M and k in K, Dk(Ek(m)) = m

### Pseudorandom Permutation

> Do not confuse PRP with PRG 
	- PRG: (Pseudorandom generator): **Takes a short random seed and output a long pseudorandom sequence**
    - Permutation cipher: A cipher using letter index permutaion operation

- In general, permutation of a set: Rearrangement of its elements

Block ciper as a permutation function:
	- A fix key, its a function that maps 2^n plaintext to 2^n ciphertexts (With unique inverse for each ciphertext)
    - In other words: C is a rearrangment of M (of itself, since M = C)
- To be a block cipher, we need a keyed pseudorandom (secure) permutation, so that:
	- The permutation should be determined by the key
    - Different keys must result into different permutations
    - The permutation should **"look random"**
- The **key random mapping**: Between plaintext and ciphertexts

> This is differnet from PRG as PRG works by using some small seed and xoring it with the key to output a Pseudorandom sequence

- Randomness: This means that cipher text should look different from random string.
- Hypothetical game: If attacker picks 2 plaintext and then recieve a ciphertext of 1 of the two, they shld not be able to distinguised which plain text was encrupted


### How it works
- Typically its not a single gigantic algorithms, but **an iteration of rounds**:
	- DES = 16 rounds, 3DES = 48 rounds, AES-128  = 10 rounds
- Two main techniques for each round: Substituition permutition network (as in AES) and Fiestel scheme (as in DES)

Block cipher rounds:
- Simpler operation
- Easy specify
- Round function f(x,k)
- The key might have gone trhough some preprocessing (expansion) before putting into round function
- Key scehdule function:
![CS2107-2-5.PNG]({{site.baseurl}}/img/CS2107-2-5.PNG)
Produce a sequence of round keys(subkeys)

> Even thou the round fucntion is the same, the key is different due to the subkey

SPN with three rounds:
![CS2107-2-6.PNG]({{site.baseurl}}/img/CS2107-2-6.PNG)



## Popular block cipher
### DES
- Block length: 64 bits
- Key length: 56
- Replace by AES
- Round function: Feistel function forming the FIESTAL NETWORK

Operations in the fiestel function:
- S box perform substitution: For confusion
- P box performing permuttition: for diffusion


![CS2107-2-7.PNG]({{site.baseurl}}/img/CS2107-2-7.PNG)
![CS2107-2-8.PNG]({{site.baseurl}}/img/CS2107-2-8.PNG)

> Exhasitive search of DES is easily done in todays time

### AES (Advance encruption system)
![CS2107-2-9.PNG]({{site.baseurl}}/img/CS2107-2-9.PNG)

- Block size: 128 bits
- Key size: 128, 192, 256 bits 9the longer, the more secure but the slower)
- SPN: Substitution and permutation networks and not fiestel:
	- In each round: Sub layer then perm layer
	- Substitition layer: BYTESUB operation
    - Permutation: ShiftRow and MixColumn operations

![CS2107-2-10.PNG]({{site.baseurl}}/img/CS2107-2-10.PNG)



## Properties


Terms meaning:
- Low error propahation: If one bit is flipped accidentally, it wont affect much
- low diffusion: Differences
- Insertion and modification: Easily inserted values and modified
- Padding: Not enough characters so need padding


### Diffusion
- two properties: Diffusion and confusion
Diffusion: A change in plaintext will affect many parts of ciphertext
	- Info from plaintext is spread over entire cipher
    - Transformation depends equally on all bits of the input

![CS2107-2-11.PNG]({{site.baseurl}}/img/CS2107-2-11.PNG)

A cipher with good diffusion:
- Attacker need to access more of the cipher text
- Block cipher: high diffusion
- Stream: Low diffusion - Due to just xor


> One bit flip can affect many parts of the cipher text


### Confusion
An attacker shld not be able to predict what happen to the cipher when **one character** in the plain text or key changes

![CS2107-2-12.PNG]({{site.baseurl}}/img/CS2107-2-12.PNG)

The input undergoes complex transformation during encryption


A good cipher: 
- Has complex functional relationship between the plaintext/key pair and the ciphertext


> Cannot predict where the change was made or was going to be made (Make it hard for the attacker known the encription)


## Block cipher modes of operation
- Block cipher can encrypt n bit plain text with n as the cipher block size
- Mode of operation: A method of encrypting messages of arbitrary size using block cipher

#### ECB
- Simple but insecure
- Just apply and concat
![CS2107-2-13.PNG]({{site.baseurl}}/img/CS2107-2-13.PNG)


BUT

- What if mi = mj?
- Attacker can tell that ci = cj
- Info is leaked 

![CS2107-2-14.PNG]({{site.baseurl}}/img/CS2107-2-14.PNG)

WHY?
- Suppose image below is divided into blocks
- Encrupted with some "Determinsitc encryption scheme" using same key
- Since deterministic: Any two plaintext blocks that are the same will encrupt into **same ciphertext**

> The white background is the same


This is because of "two key problem":
- Same key used
- Same plaintext block always give the same cpher block
- Due to deterministic encryption process


> We cant choose random IV for each block as the size of final cipher will increase

### Mode of operation: CBC (Cipher block chaining) on AES
- Mode of operation describes how the blocks are to be linked so that diff blocks at diff location would give diff cipher text even if the blocks have same content

![CS2107-2-15.PNG]({{site.baseurl}}/img/CS2107-2-15.PNG)

- Borrow the output from the previous round as the IV for the next round

### Mode of operation: CTR (counter)
![CS2107-2-16.PNG]({{site.baseurl}}/img/CS2107-2-16.PNG)

### Double DES and meet in the middle attack
- 2DES: 2 keys
	- Encrupt key one and then kley 2
    - Key length: 112 bits (Hard to brute force)

BUT, there is the meet in the middle attack.
Just get two computer and try to crack the code from the plaintext side and the encryped side. Then compare the two to see if it matches (Meet in the middle)

### Triple DES
- 3 keys use: 3 independent keys
- double keys: 2 independent keys

![CS2107-2-17.PNG]({{site.baseurl}}/img/CS2107-2-17.PNG)

Compared to AES: The 3DES is less efficient:
- Sluggish in software
- Can only encrypt 64 bit blocks at time

### Padding Oracle attack
AES CBC mode is not secure agaisnt this padding attack

Attacker can send queries and Oracle will output the answer
- Encryption oracle: On query containing plaintext x, oracle output ciphertext
- Decryption: Query with ciphertext c


The attacker have:
- A cipher text with IV and C
- Access to padding oracle

Goal:
- Get the plaintext

Notes about secret key:
- The ciphertext is encrypted with k
- Padding oracles knows k
- The attacker does not know k

Padding otacle:
- Query: A ciphertext
- Output: yes or no
	- Yes, if the plaintext is in correct padding format
    - No, otherwise




#### Padding format
![CS2107-2-18.PNG]({{site.baseurl}}/img/CS2107-2-18.PNG)

### Padding using PKCS#7
![CS2107-2-19.PNG]({{site.baseurl}}/img/CS2107-2-19.PNG)

> The number of blocks of padding is encoded as the value for that blocks

### AES CBC Mode
- Not secure agaisnt padding oracle attack
- Attacker has IV\\C: 1 block of IV and 1 block of c
- In this example, attacker already knows the size of the plaintext padding : 3
- Generate some t:
![CS2107-2-21.PNG]({{site.baseurl}}/img/CS2107-2-21.PNG)


### Why it works
Attacker wants to find the value of X5:

![CS2107-2-22.PNG]({{site.baseurl}}/img/CS2107-2-22.PNG)
![CS2107-2-23.PNG]({{site.baseurl}}/img/CS2107-2-23.PNG)

> Rexoring the padding gives us a fix value
>
	- Imagine the padding is 03
    - Encrypting this padding with the key 04 gives 07
    - if the attacker tries to get the key,
    they can make the inference that 07 = 04 xor 03

WORKING:

![CS2107-3-1.PNG]({{site.baseurl}}/img/CS2107-3-1.PNG)
![CS2107-3-2.PNG]({{site.baseurl}}/img/CS2107-3-2.PNG)

#### Additional remarks
- Attack modifies iv to iv`

Lets say oracle say yes.

- What is the produce accepted plaintext?
	- `X = I xor IV`
- We can find the X5 by working backwards
	- Given the padding oracle
- Extend the algo to find all the plaintext
- Algo need to know plaintext length: It is possible to determine the length
- The attack is practical, there are real world protocols between a client and server that performs this
> If the client submits a ciphertext whose plaintext is not padded correctly, the server will reply with an error message


#### Important lessons from padding oracle attack
- There are ways for attacker to exploit seemingly useless infomation
- Wrong use of encryption: encryption is used to protect integrity

# Security analysis of a cipher (LECTURE 2)
- Security analyisis of a cipher done to respect to:
	- Threat model:
    	- Assumption about attacker's capabilities
        - Categorise into black boxes
- Goal/Security guarentee:
	- What is the attacker trying to do
    - What does he want
    
Black box:
- Query operation to the cipher
- A query to a cipher: The operation taht sends input models
- Attackers capabilities
	- Ciphertext only
    - Known plaintext

![CS2107-3-3.PNG]({{site.baseurl}}/img/CS2107-3-3.PNG)

Gray Box mdels:
Attacker has access to cipher implementation.
- Side channel:
	- Source of info that dependens on the implementation
    - Observer and measure analog characteristics of a cipher implementation
    - Type side channel: Executive power consumption
- Invasive attack
  - More powerful that side channel attacks
  - More expensive: More sophisticated equipment

# Cryptography pitfalls: Attacks on cryptosystem implementation

## Resuing IV, wrong choices of IV, one time pad key

### Reusing and wrong choice
- Some applications overlook IV generation
- Same IV might be reused

> For example, to encrypt a file F, the IV is derived from the filename. It is quite common to have files with the same file name


The best is to get good values for IV


### Reusing one time pad key
- Verona project


## Predicatable secret key generation

### Random Number generation
Scenario 1:
- Coding program for simulation system
- In program need a sequence of random numbers
- How to get random numbers


Scenario 2:
- Coding program for security system
- Need a random number for like a temp secret key
- How to get these random numbers?


> We need strong random numbers for cripto
##### Java shit
![CS2107-3-4.PNG]({{site.baseurl}}/img/CS2107-3-4.PNG)

## Design your own cipher
Do not make ur own cryptosystem or make a slight modification to existing scheme unless you have in depth knowledge of the topic

# Kerchjoff principle vs Security through Obscurity

> A system should be secure even if everything about the systen except the secret key is a public knowledge

Useful:
- Easier to keep secret key vs secret algo
- easeier to change secret key vs secret algo
- Standardised algo allows easy deployment
- Public scrutiny on open algo: Peer revie and security validation

##### Security through obscurity
- To hide the design of the system in order to achieve security
> Is it good or bad?

#### Examples
- RC4: 
	- Intro in 1987 and algo is trade secret
    - 1994: Descp of algo was anonymously posted in mailing group
- MIFARE Classic:
	- A contactless smartcard widely used in Europe employed a set of protocols and algo
    - Reversed engineered in 2007
- Usernames:
	- Not secrets
    - Not advisable to publish all the usernames
- Computer network structure and settings:
	- Location of firewalls and rules
    - These are not secrets and many users within org would have known the settings
    - Still not advisable to them
- The actual program used in a smart card:
	- Not advisable to publish it
    - If prog is published, an adversary may be able to identity vulnerability that is prev unknown or carry out side channel attacks
    - A sophisticated advisory may be able to reverse engineer the code 

> We can use it but its only be use as one layer >_<

- One layer in defense in depth strategy
- Deter or discourage novice attackers but ineffective agaisnt attackers with high skill and motivation
- System must remain secure even if everything about it except its key is known

# Slides

<iframe src="https://drive.google.com/file/d/1v9Exazq6MwuyWJ5wsX0cOZGlJU_p3_EG/preview" width="640" height="880"></iframe>
