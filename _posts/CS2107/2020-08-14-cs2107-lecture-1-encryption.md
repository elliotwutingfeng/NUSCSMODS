---
layout: post
published: false
title: 'CS2107 - Lecture 1: Encryption'
---

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
### Vigenere Cipher
### Permutation Cipher
### One time Pad

