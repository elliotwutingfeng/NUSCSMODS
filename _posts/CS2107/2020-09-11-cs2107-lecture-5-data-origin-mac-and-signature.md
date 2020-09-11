---
layout: post
published: true
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
- If we use SKC then any two enties must share a secret key
	- Many keys are required expecially if the no of entities is large
    - Establishing all secret key is also difficult

![CS2107-4-5.PNG]({{site.baseurl}}/img/CS2107-4-5.PNG)

> But if we use the public key to encrypt, how do we make it such that someone cant just use the public key to decrypt and get the plaintext? What is the inner working of this such that the attacker needs the secret key since the encrypter only has access to one key (Not the private)

## RSA
- Basic form 
- Stil requires other stuff like padding
- Integers represented in binary
- When a key is 1024 bits, it means that it can be represented using 1024 bits under binary representation
(3 bit int is a value from 0 to 7)

### Set up
1. Owner choose 2 large primes p and q and compute n = pq as the public composite modules
	- Note that values of p and q is secret
2. The owen rqndomly choose a encryption exponent e s.t gcd(e, fi(n)) = 1 and e is relatively prime to fi(n)
	- fi(n) = (p-1)(q-1) is the euler totient function
3. The owner determins the decryption exponent d where de = 1 (mod fi(n)) ie d = e^-1 (mod fi(n))
	- p and q can throw away
4. The owner publishes (n, e) as her public key and keep (n,d) as private

### Encryption and decryption
- Public key: (n,e)
- Private: (n,d)
- Encryption: Given message m, the ciphertext c is c = m^e (mod n)
- Decryption: Given a cipher text c, the plaintext m is m= C^d (mod n)

![CS2107-4-6.PNG]({{site.baseurl}}/img/CS2107-4-6.PNG)

### Correctness
![CS2107-4-7.PNG]({{site.baseurl}}/img/CS2107-4-7.PNG)

### Example
![CS2107-4-8.PNG]({{site.baseurl}}/img/CS2107-4-8.PNG)

### Note
- RSA has a property where we can use the decryption of key d to encrypt and then the encryption key e to decrypt
- This property is not the same in other public key scheme


Algo Efficiently issues:
![CS2107-4-9.PNG]({{site.baseurl}}/img/CS2107-4-9.PNG)


## Security of RSA
- There is a factorisation problem
- The problem of finding private key from publick key is as difficult as the factorisation.
> We need p and q to derive d

- RSA problem: Finding the plaintext from ciphertext and publick key

![CS2107-4-10.PNG]({{site.baseurl}}/img/CS2107-4-10.PNG)

> 700 bit number is no longer safe/

![CS2107-4-11.PNG]({{site.baseurl}}/img/CS2107-4-11.PNG)
![]({{site.baseurl}}/img/CS2107-4-12.PNG)![CS2107-4-12.PNG]({{site.baseurl}}/img/CS2107-4-12.PNG)


### Post Quantum cyptography
- In quantum computer can factosize and perfrom discrete log in polytime
- Both RSA and discrete log based PKC will be broken with quantum computer
- Post quantum cryptogrpahy
PKC Schems that are secure agaisnt quantum computer
- Lattice based crypto

- Multivariate crypto

### Padding RSA
- IV is required
- Addiitional mechanism must be use
- Homomorphic property

![CS2107-4-13.PNG]({{site.baseurl}}/img/CS2107-4-13.PNG)


## Improper RSA usage
Consider a sample scenario:
" For his final year project, bob is tasked to write an app that employs an end to end encryption to send images from a mobile phone to another mobile phone over wifi. The sender and recipient use SMS to establish the required symmetric key.:

- Bob feels that RSA is cool
- Instead of employing AES, Bob employs RSA as the encryption schem: The publick seceret key pair is treated as symmetric key
- Bob claims rsa is more secure than aes, it can be proved to be difficult as factorisation which is believe to be hard
- RSA implementation: To encrypt a large image, bob dividese the files into chunks and apply RSA to each chunk
- Implmentation diagram:
![CS2107-4-14.PNG]({{site.baseurl}}/img/CS2107-4-14.PNG)

> What is wrong?

### Efficiency and performance
- RSA is slower than AES

Solution:
> Use AES first (For a large file)

![CS2107-4-15.PNG]({{site.baseurl}}/img/CS2107-4-15.PNG)



### ECB with RSA
- Dividing the plaintext into piece and independently apply encryption to each of them could leak important info
-Suppose the image below is divided into blocks and encrypted with some deterministic encryption scheme using the same key
- SInce it is deterministic, any two plaintext blocks that are exactly the same will be encryption into the same ciphertext
![CS2107-4-16.PNG]({{site.baseurl}}/img/CS2107-4-16.PNG)


### Security of RSA
1)
- Not necessarily more secure than AES
- It can be shown that getting the private key from the publick key is difficulkt as factorisation
- But it is not known whether the prblem of getting the plaintext from the ciphertext and public key


2)
- RSA has to be modified so that different encryptions of the same plaintext lead to different ciphertext


3)
- Factorisation can be done by a quantum computer
	- RSA is broken by quantum computer
    - It is not clear how a quantum computer can be used to break AES
    

# Crypto background 2: Hash and keyed-hash
## (Unkeyed) Hash 
![CS2107-4-17.PNG]({{site.baseurl}}/img/CS2107-4-17.PNG)

- A function that takes an arbitrarily ling message as input and outputs a fixed size (160 bits) digest
- Note that a hash function takees no key
- A cryptographic has must meet some secuirty requiremetns
- Do not use non cryptographoc has function such as:
	- Taking selected bits from the data
    - CRC checksum

![CS2107-4-18.PNG]({{site.baseurl}}/img/CS2107-4-18.PNG)

> One way - It is easy to get one direction but is hard to go the other way

Examples:
- SHA-1
- SHA-3



## Keyed hash
A keyed hash is a function that takes an arb long message and secret key as input and outputs a fixed size. MAC
{IMG}


![CS2107-4-19.PNG]({{site.baseurl}}/img/CS2107-4-19.PNG)

Examples:
- CBC - MAC
- HMAC



# Data integrity: Hash without secret key
Example:
- Someone download a software
- Someone software hosted by 3rd party
- How do we known the autentictiy of the file

![CS2107-4-21.PNG]({{site.baseurl}}/img/CS2107-4-21.PNG)

- We need the digest to check if its correct
![CS2107-4-22.PNG]({{site.baseurl}}/img/CS2107-4-22.PNG)

> Attacker can find another F' that givves the same digest

- Integrity is not about authenticity




# Data Authenticity (Mac, signature)
## MAC
- MAC might be also modified by attacker
![CS2107-4-23.PNG]({{site.baseurl}}/img/CS2107-4-23.PNG)

- Typically MAC is appended to F, then they are stored as a single file or transmitted together through a communication channel, hence MAC is also called authenticity tag
## Signature
![CS2107-4-24.PNG]({{site.baseurl}}/img/CS2107-4-24.PNG)

- Signing the private key is used
- Verification the public key is used

### What is special about signaure
- We can view digital signature as the counterpart of handwritten signature in legal document
	- Document is authentic or certified if it has the correct handwritten signature
    - No one except the authentic signer can forge the signaure
- In addition to authenticity, signature scheme also achieves non repudiation:
	- Assurance that soemone cannot deny his or her previous commitments or actions

![CS2107-4-25.PNG]({{site.baseurl}}/img/CS2107-4-25.PNG)

> MAC: We cannot force ALICE to admit that the MAC come from her, she can argue that it come from BOB

> DIgital signature: It is confirm from ALICE, to generate the signature.. only ALICE can generate it thus it can only be from her

Most signature scheme consist of two components:
- AN unkey hased and sign/verify algo

![CS2107-4-26.PNG]({{site.baseurl}}/img/CS2107-4-26.PNG)
![CS2107-4-27.PNG]({{site.baseurl}}/img/CS2107-4-27.PNG)

Popular Signature scheme:
- Sign(): Private key encryption
- Verify(): Decryption

# Some attacks and pitfalls
## Birthday attack on hash
- Hash function are designed to make a collision difficult to find
- Collision involves two different messages that give the same digest
- But all hash function are subjected to birthday attack (Similiar to exhastive search on encryption scheme)

### Birthday Paradox
![CS2107-4-28.PNG]({{site.baseurl}}/img/CS2107-4-28.PNG)


## Use encryption for authenticity
# Application of hash: Password file protection
