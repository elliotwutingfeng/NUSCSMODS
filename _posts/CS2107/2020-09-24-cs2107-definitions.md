---
layout: post
published: false
title: CS2107 - Definitions
---
# Important Definitions (For everything)

- Confidentiality: The infomation of the users
- Authentic: The claimed entity is sassured by supporting evidence
- Authentication: The process of assuring that the comunicating entity or the origin of a piece of infomation is the one that it claims to be (See Lecture 4/5 )
- Authenticity: The condition of being authentic
- Integrity:  Modification of process/infomation
- Availability:  Availability of the services for the user
- non-repudiation: Gurantees only the specific person can access 
- Threat: A set if circumstances that has the potential to cause loss or harm
- Security is the protection of assets:
	- Hardware
    - software
    - data 
    - infomation
    - Reputation: Which is intangible
- Vulnerability: A weakness in the system
- Cryptography: Study of techniques in secuiring communications in the presence of advisaries (Bad ppl). 
- Control: A control, countermeasure, security mechanism is a mean to counter threats
	- Physical control: Facilities protection, security guards, locks, monitoring, environmental controls, intrusion detection
    - Technaical control: Logical access control, encryption, security devices, identification and authentication
    - Administrative controls: Policies, standards procedures, guidelines, screening personnnel, security-awareness training


- Trade of in securiyt:
	- Ease of use: Security mechanism interfere with working patterns users originally familiar with
    - Performance: Security mechanisms consusmes more computing resouirces
    - Cost: Secuirty meachnism are expensive to develop
    
## Ciphers

- Monoalphabetic cipher: THe substitution is fixed for each letter of the alphabet
- Polyalphabetic cipher: The substituiton is not fixed for each letter of alphabet if there is more than one of the same...
- Shift cipher: A type of substitution cipher
- Ceaser cipher: A shift cipher with a shift of 
- Transposition cipher: Apply a secret permutation to the characters in each block by shuffling
- Encryption query: Takes plaintext return cipher
- Decryption query: Takes cipher return plaintext
- COA (Cipher text only attackers): Can see ciphertext only
- KPA (Known-plaintext attacker): Can observe ciphertext and do know the associated plaintext
- PRG (Pseudorandom generator): Takes a short random seed and output a long pseudorandom sequence
- PRP (Pseudorandom Permutation): Key random mappings between plaintext and ciphertext, is a function that cannot be distinguished from a random permutation (that is, a permutation selected at random with uniform probability, from the family of all permutations on the function's domain) with practical effort.
- SPN:  In cryptography, an SP-network, or substitution–permutation network, is a series of linked mathematical operations used in block cipher algorithms such as AES, 3-Way, Kalyna, Kuznyechik,
- Block cipher:
	- Diffusion: A change in plaintext will affect many parts of the ciphertexts
    - Confusion: Attacker cannot predict what will happen to the ciphertext when one character in the plaintext or key changes
- Mode of operation: A method of encrypting messages of arbitrary size using block cipher
- Cryptography: Study of techniques in secuiring communications in the presence of advisaries (Bad ppl). 
- Control: A control, countermeasure, security mechanism is a mean to counter threats
	- Physical control: Facilities protection, security guards, locks, monitoring, environmental controls, intrusion detection
    - Technaical control: Logical access control, encryption, security devices, identification and authentication
    - Administrative controls: Policies, standards procedures, guidelines, screening personnnel, security-awareness training


- Trade of in securiyt:
	- Ease of use: Security mechanism interfere with working patterns users originally familiar with
    - Performance: Security mechanisms consusmes more computing resouirces
    - Cost: Secuirty meachnism are expensive to develop
    
## Ciphers

- Monoalphabetic cipher: THe substitution is fixed for each letter of the alphabet
- Polyalphabetic cipher: The substituiton is not fixed for each letter of alphabet if there is more than one of the same...
- Shift cipher: A type of substitution cipher
- Ceaser cipher: A shift cipher with a shift of 
- Transposition cipher: Apply a secret permutation to the characters in each block by shuffling
- Encryption query: Takes plaintext return cipher
- Decryption query: Takes cipher return plaintext
- COA (Cipher text only attackers): Can see ciphertext only
- KPA (Known-plaintext attacker): Can observe ciphertext and do know the associated plaintext
- PRG (Pseudorandom generator): Takes a short random seed and output a long pseudorandom sequence
- PRP (Pseudorandom Permutation): Key random mappings between plaintext and ciphertext, is a function that cannot be distinguished from a random permutation (that is, a permutation selected at random with uniform probability, from the family of all permutations on the function's domain) with practical effort.
- SPN:  In cryptography, an SP-network, or substitution–permutation network, is a series of linked mathematical operations used in block cipher algorithms such as AES, 3-Way, Kalyna, Kuznyechik,
- Block cipher:
	- Diffusion: A change in plaintext will affect many parts of the ciphertexts
    - Confusion: Attacker cannot predict what will happen to the ciphertext when one character in the plaintext or key changes
- Mode of operation: A method of encrypting messages of arbitrary size using block cipher
- Two key problem: Using the same key for two encryption = can break the ciphertext

## Authentication
- Sniff: small program that listens to all traffic in the attached network(s), builds data streams out of TCP/IP packets, and extracts user names and passwords (Eves dropping)
- Spoof: When someone tries to introduce himself as another person
- Phising: User is tricked to voluntarily send the password to the attack over the network
- Reply attack: A replay attack (also known as playback attack) is a form of network attack in which a valid data transmission is maliciously or fraudulently repeated or delayed.

## CA
- Certification chain: A list of certifcicates starting with an end entity certificate followed by one or more CA certificate.