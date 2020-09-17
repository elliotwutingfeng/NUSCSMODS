---
layout: post
published: true
title: 'CS2107 - Lecture 6: PKI + Channel security'
---
# Public key distribution
PKC-based method to assure the authenticity of the downloaded program:
- The developer signed the file using his private key
- A user who has downloaded the file from unverified source can verify the authenticity of the file using the developer's public key

Motivation: 




Securely distributed/broadcast public keys which we can use for encryption(confidentiality) and signature verfication (authentication)

### Secure channel requirement


### Possible public key distribution methods
1. Public announcemnet
2. Publicly available directory
3. Public key infrastructure


#### public announcement
- Broadcast public key
- e.g send via email or website
- Many ownders list their keys in blog

Limitation:
- Not standardized: Cannot verify the public key when needed
- Need trust the entity distributing the PK

#### Publicy available directory
- Search the public directory by query a server


Limitation:
- Anyone can post their pk to the server
- Not easy to have secure public directory, how does server verify that the info sent to it is correct
- Some entity needds to be entrusted
	- Server
    - User

#### PKI + certificate
- PKI is a standardised system that distributed public keys
- PKI Objectives:
	- To make PK crypto deployable on large scale
    - To make public keys verifiable without requireing any two communicating parties to directly trust eqach other
    - To manage public and private key pairs throughout their entire key lifecycle
- PKI is centered around two important components/notions
	- Certificate
    - Certificate/ Certification Authority (CA)
- PKI provided a mechanism for trust to be extended in a distributer manner starting from root CA


# Public key infrastructure (PKI)
## Certificate

CA:
- Issues and signs digital certificates
- Keeps a directory of public keys
- Has its own public private key pair: We assume that the CA public key has been securely distributed to all entities involved
- Most OSes and browsers have a few preloaded CAs public keys: They are known as root CA
- Stringent operational requirements for CA


Content and usage:
- Certificate must contain at least:
	- Owner identity
    - Public key of owner
    - Time window till this cert is valid
    - Signature of CA
    
Without certificate:



With certificate:


Role:
- CA binds an entity with his public key prior to verfication point
- User can obtain the dev;s PK can verifies its authenticity without a connection to the CA
- BUT: THere is still a need to check that the cert has not been revoked


#### X.509 Digital certificate standard


## CA and Trust relationship

Responsibility:
- Verify the info is correct
- Manual checking and thus could be costly


Check:
- Domain validation (DV) SSL certificate: Issue if the purchaser can demostrate the right to adminsitratively manage a domain name
- Organisation validation (OV) SSL certificate: Issued if purchaser additionally has an organisation actual existence as a legal entity


# Limitiation/attacks on PKI
