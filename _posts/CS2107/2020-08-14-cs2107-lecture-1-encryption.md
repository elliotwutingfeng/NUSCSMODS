---
layout: post
published: true
title: 'CS2107 - Lecture 1: Encryption'
---

- Confidentiality - The infomation of the users
- Integrity -  Modification of process/infomation
- Availability - Availability of the services for the user
- non-repudiation - Gurantees only the specific person can access 

# Definition
An encryption scheme also known as cipher consist of envryption and decryption.
![]({{site.baseurl}}/img/CS2107-1-1.PNG)

Requirements:
- Correctness: For any plaintext x and Key
- Security: Given the ciphertext, it is difficult to derive usefull infomation of the key and plain text
- Performance requirements: Efficiently computed
![CS2107-1-2.PNG]({{site.baseurl}}/img/CS2107-1-2.PNG)


#### Example
![CS2107-1-3.PNG]({{site.baseurl}}/img/CS2107-1-3.PNG)


## Cryptography
Cryptography is the study of techniques in securing communication in the present of adversaries.

Encryption is one of the basics of cryptography

Applications:
- Secure communication/transaction
- Disk Encryption
- Content protection
- Password
- Digital signature
- Cryptocurrency: E.g Bitcoin

### Charactersin Cryptography
- Alice: Originator of message
- Bob: Recipient
- Eve: Eaves dropper, listen to sent message
- Mallory: Mallicious and modify message
![CS2107-1-4.PNG]({{site.baseurl}}/img/CS2107-1-4.PNG)
> Sometimes these characters might not be human

## Classical cipher
### Substitute Cipher
![CS2107-1-5.PNG]({{site.baseurl}}/img/CS2107-1-5.PNG)

Its just mapping a value to another value

Some terms:
- The key space: The set of possible keys
- Key space size: The total number of possible keys
- The key size or key length: The number of bits required to reperesent a particular key
- For subsitution ciper:
	- The key space
    - The space size : 27!
    - The key size : log2(27!) = 94 bits

> The key is the a,b,c

> This is called a trivial key, it is a trivial permutaion




### Vigenere Cipher
### Permutation Cipher
### One time Pad
