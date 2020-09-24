---
layout: post
published: true
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


# Tutorial terms

## 1
- Cryptology = Cryptography + Cryptanalysis.

- The National Security Agency (NSA): a national-level intelligence agency of the US Dept of Defense, which is responsible for global monitoring, collection, and processing of information and
data for foreign intelligence and counterintelligence purposes, specializing in a discipline known as signals intelligence (SIGINT).

- The National Institute of Standards and Technology (NIST): a measurement standards laboratory, and a nonregulatory agency of the US Dept of Commerce, whose mission is to promote innovation and industrial competitiveness.

- Cryptography backdoor: a method, often secret, of bypassing normal encryption in a cryptosystem. It allows an intruder to access the plaintext without having the correct user credentials.

- Key escrow: an arrangement in which the keys needed to decrypt encrypted data are held in escrow so that, under certain circumstances, an authorized third party may gain access to those keys.

- Decryption order: an order that forces suspects to decrypt their encrypted data or give up their keys.

- Whitfield Diffie: one of the pioneers of public-key cryptography; co-inventor of Diffie-Hellman key exchange; won the 2015 Turing Award.

- Ron Rivest: co-inventor of the RSA algorithm; inventor of the symmetric-key encryption algorithms RC2/RC4/RC5; inventor of the MD2/MD4/MD5/MD6 cryptographic hash functions; co-author of \Introduction to Algorithms" book; won the 2002 Turing Award.

- Alice, Bob, Eve, Mallory: Check https://en.wikipedia.org/wiki/Alice_and_Bob#Cast_of_characters.

- Trent (or Ted): a trusted arbitrator as a neutral third party

## 3

- Graphical password: A graphical password or graphical user authentication is a form of authentication using images rather than letters, digits, or special characters. The type of images used and the ways in which users interact with them vary between implementations.

- Covert channel: In computer security, a covert channel is a type of attack that creates a capability to transfer information objects between processes that are not supposed to be allowed to communicate by the computer security policy. The term, originated in 1973 by Butler Lampson, is defined as channels "not intended for information transfer at all, such as the service program's effect on system load," to distinguish it from legitimate channels that are subjected to access controls by COMPUSEC.

- Side channel attack: In computer security, a side-channel attack is any attack based on information gained from the implementation of a computer system, rather than weaknesses in the implemented algorithm itself (e.g. cryptanalysis and software bugs). Timing information, power consumption, electromagnetic leaks or even sound can provide an extra source of information, which can be exploited.

- End to End encryption: End-to-end encryption (E2EE) is a system of communication where only the communicating users can read the messages. In principle, it prevents potential eavesdroppers – including telecom providers, Internet providers, and even the provider of the communication service – from being able to access the cryptographic keys needed to decrypt the conversation.


## 4

- Single sign on (SSO): Single sign-on (SSO) is an authentication scheme that allows a user to log in with a single ID and password to any of several related, yet independent, software systems. It is often accomplished by using the Lightweight Directory Access Protocol (LDAP) and stored LDAP databases on (directory) servers. A simple version of single sign-on can be achieved over IP networks using cookies but only if the sites share a common DNS parent domain.

- Hardware randomnumber generator (HRNG): In computing, a hardware random number generator (HRNG) or true random number generator (TRNG) is a **device** that **generates random numbers from a physical process**, rather than by means of an algorithm. Such devices are often b**ased on microscopic phenomena that generate low-level, statistically random "noise" signals, such as thermal noise, the photoelectric effect, involving a beam splitter, and other quantum phenomena**. These stochastic processes are, in theory, completely unpredictable, and the theory's assertions of unpredictability are subject to experimental test. This is in contrast to the paradigm of pseudo-random number generation commonly implemented in computer programs.

- Quantum random number generator (QRNG): Better than HRNG (they heavily rely on post-processing algorithms – that are deterministic thus vulnerable) , Quantum RNGs exploit elementary quantum optic processes that are fundamentally probabilistic to produce true randomness. As the quantum processes underlying the QRNG are well understood and characterized, their inner working can be clearly modelized and controlled to always produce unpredictable randomness.

- Iris scan: Iris Recognition uses a camera, which is similar to any digital camera, to capture an image of the Iris. 

- Retina scan: Retinal Scanning requires a very close encounter with a scanning device that sends a beam of light deep inside the eye to capture an image of the Retina.

- Retina vs Iris scan:
		  
          Similarities:

          Low occurrence of false positives
          Extremely low (almost 0%) false negative rates
          Highly reliable because no two people have the same iris or retinal pattern
          Speedy results: Identity of the subject is verified very quickly
          The capillaries in the iris and retina decompose too rapidly to use a amputated eye to gain access

          Differences:

          Retinal scan measurement accuracy can be affected by disease; iris fine texture remains remarkably stable
          An iris scan is no different than taking a normal photograph of a person and can be performed at a distance; for retinal scanning the eye must be brought very close to an eyepiece (like looking into a microscope)
          Iris scanning is more widely accepted as a commercial modality than retinal scanning
          Retinal scanning is considered to be invasive, iris is not














