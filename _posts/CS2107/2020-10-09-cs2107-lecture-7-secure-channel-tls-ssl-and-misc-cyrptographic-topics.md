---
layout: post
published: false
title: 'cs2107 - Lecture 7: Secure channel, TLS/SSL and Misc Cyrptographic topics'
---
# Strong authentication

Password is weak authentication: Any eavesdropper can get the password and replay it.

- The password: The secret shared and exchanged between Alice and Bob
- Is it possible to have a mechanism that ALice can prove to Bob that she knows the secret without revealing the secret


## SKC Bashed Challenge response
Suppose Alice and Bob have a shared secret key k, and both of them agree on an encryption scheme say AES

1. ALice sends Bob a hello message
2. (Challenge) Bob randomly picks m and send to Alice:
	y = Ek(m)
3. (Response) ALice decrypt y to get m and then sends m to Bob
4. Bob verifies that the message received is indeed m is so accepts other wise rejects


- Even if Eve can obtain the communication between Alice and Bob, he cant get the secret key k
- Eve cannot replay the response either: challenge m is randomly chosen and likely to be different in the next authentication session
- The protocol only authenticates alice: Unilateral authentication
- There are protocols to verify both parties: Mutual authentication

> What is freshness in the context of authentication protocol

Using PKC:
1. ALice sends Bob a hello message
2. (Challenge) Bob choose random number r and send to Alice:
	 "ALice, here is your challenge, r"
3. (Response) ALice use her private key to sign r and sends to bob: Sign(r), Alice's certificate
4. Bob verifies Alice's certificate, extracts Alice's public key from the certificate then verifies that the signature is correct

- Eve cant know nor derive Alice private key and replay the response because the challenge r is likely to be differtent
- The value r is also known as cryptographic nonce

> The shown protocol have omitted many details, designing a secure authentication protocol is not easy

### Is authentication alone sufficient
- There might be mallory who can modify messages and want to pretend to be ALice


- After Bob is convinced that he is communicating with ALice, Mallory interrupts and takes over the channel whilst pretending to be Alice


- Strong authentication: Assumes Mallory is unable to interrupt the session
- For applications whereby Mallory can interrupt the session, we thus need something more
- The outcome of the authentication process must be the new secret k (Session key) establisedd by Alice and Bob



# Key exchange and authenticated key exchange
# Putting all together: Securing a communication channel
# Putting all together: TLS/SSL
# Authenticated Encryption
# Time-memory tradeoff for dictionary attack
# Birthday attack variant
# Other interesting cryptography topics
#
