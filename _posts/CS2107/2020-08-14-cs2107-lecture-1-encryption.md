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

#### Encryption/Decryption
![CS2107-1-7.PNG]({{site.baseurl}}/img/CS2107-1-7.PNG)


#### Attacks on cipher
- Attacker goals is to 
	- find the key: If found, the cipher is broken
    - To obtain some info about the plaintext
- Before commencing an attack, the attacker needs to access to some info such as:
	- A large number of ciphertexts that are all encrypted using the same key "Ciphertext only" or
    - Pairs of cuphertext and the corresponding plain text, "known plaintext"

#### Exhastive search (brute force) attack
- Search the key : Examine all possibble keys one by one
- Exhastive search is infeasible normally
- For some moden cipers like DES, it is feasible to break it using exhastive search
- Sophisticated attacks exploit the properties of the encryption scheme to speed up proccess, "analytical attacks"


Example: Known plain text scenario
- Consider the substituition ciper of size 27
- Attacker has access to ciphertext c and plain text X
- Let S be set of all possible subsitiution table
![CS2107-1-8.PNG]({{site.baseurl}}/img/CS2107-1-8.PNG)

> It will take very long because we are trying for each permutaion of table

- Running time depends on size of key space S
- On avg: 2^93 loops

#### Better attack on know plain text
- Attacker can figure out the entries in the key as long as given a plaintext and cipher text
- If the attacker has access to pais of ciphertext and their corresponding plaintext, they can guess the key
- Substitution ciper is insecure under known plaintext attack

** **SUBSTITUTION CIPHER IS INSECURE** **


#### Remarks
- There is requirement to know the corresponding plaintext
	- Attacker does not need to know the full plaintext but only the first few bytes of the plaintext are enough
- Guessing:
	- Email data: certain words in its header are fix e.g "from"
    - Many network protocol with fix headers
    - Commonly used words like "Weather" and "Nothing to report"


#### Exhastive search: Ciphertext only

- Only have ciphertext
- Knows plain text are english sentence

![CS2107-1-9.PNG]({{site.baseurl}}/img/CS2107-1-9.PNG)

- Evantually will find the key
- There is small probability that the above algo finds a wrong key
- For sufficiently long cipher text, the probability that a wrong key will give meaningful english setence is v low.

![CS2107-1-10.PNG]({{site.baseurl}}/img/CS2107-1-10.PNG)

> They can map frequently occuring letters to the ciphertext to the frequently occuring letters of english



### Vigenere Cipher
### Permutation Cipher
### One time Pad
