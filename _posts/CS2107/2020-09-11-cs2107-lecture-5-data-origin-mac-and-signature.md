---
layout: post
published: false
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
- Encryption: Given message m, the ciphertext c is c = m^e (mod n)##



## Security of RSA
## Improper RSA usage

# Crypto background 2: Hash and keyed-hash
## Hash 
## Keyed hash


# Data integrity

# Data Authenticity (Mac, signature)
## MAC
## Signature

# Some attacks and pitfalls
## Birthday attack on hash
## Use encryption for authenticity
# Application of hash: Password file protection 
