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




## Popular block cipher
## Properties
## Block cipher modes of operation
## Examples of attacks on block ciphers
