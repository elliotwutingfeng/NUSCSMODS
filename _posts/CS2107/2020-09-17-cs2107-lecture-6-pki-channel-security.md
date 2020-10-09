---
layout: post
published: true
title: 'CS2107 - Lecture 6: PKI + Channel security'
---
# Public key distribution
PKC-based method to assure the authenticity of the downloaded program:
- The developer signed the file using his private key
- A user who has downloaded the file from unverified source can verify the authenticity of the file using the developer's public key
![CS2107-5-1.PNG]({{site.baseurl}}/img/CS2107-5-1.PNG)



Motivation: 
![CS2107-5-2.PNG]({{site.baseurl}}/img/CS2107-5-2.PNG)

Someone intercepted bob and pretends to be Bob, thus the public key sent is from Mallory


Securely distributed/broadcast public keys which we can use for encryption (confidentiality) and signature verfication (authentication)

### Secure channel requirement
![CS2107-5-3.PNG]({{site.baseurl}}/img/CS2107-5-3.PNG)


1)Broadcsting Keys 2)Publishing key 3) Timing requirement


Compared to symmetric key setting, we do not need to broadcast the private key. It is okay if the public key is known.

### Possible public key distribution methods
1. Public annoncement
2. Publicly available directory
3. Public key infrastructure


#### Public announcement
- Broadcast public key
- e.g send via email or website
- Many ownders list their keys in blog

Limitation:
- Not standardized: Cannot verify the public key when needed (Not everyone has the same medium)
- Need trust the entity distributing the PK (Like the website)

> How do we know the website can be trusted

#### Publicy available directory
- Search the public directory by query a server
![CS2107-5-4.PNG]({{site.baseurl}}/img/CS2107-5-4.PNG)


Limitation:
- Anyone can post their pk to the server (Need to be regulated)
- Not easy to have secure public directory, how does server verify that the info sent to it is correct
- Some entity needs to be entrusted
	- Server: Giving the correct PK
    - User: not an imposter

#### PKI + certificate
- PKI is a standardised system that distributed public keys
- PKI Objectives:
	- To make PK crypto deployable on large scale
    - To make public keys verifiable without requiring any two communicating parties to directly trust eqach other
    - To manage public and private key pairs throughout their entire key lifecycle
- PKI is centered around two important components/notions
	- Certificate
    - Certificate/ Certification Authority (CA)
- PKI provided a mechanism for trust to be extended in a distributer manner starting from root CA


# Public key infrastructure (PKI)
## Certificate

CA (Certificate Authority):
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
![CS2107-5-5.PNG]({{site.baseurl}}/img/CS2107-5-5.PNG)

With certificate:
![CS2107-5-6.PNG]({{site.baseurl}}/img/CS2107-5-6.PNG)

Bob doesnt need to contact the CA..


Role of certificate(No required directory sever):
- CA binds an entity with his public key prior to verfication point
- User can obtain the dev's PK can verifies its authenticity without a connection to the CA
- BUT: THere is still a need to check that the cert has not been revoked
	- OCSP responder (Online CRL distribution points)


#### X.509 Digital certificate standard
![CS2107-5-7.PNG]({{site.baseurl}}/img/CS2107-5-7.PNG)
![CS2107-5-8.PNG]({{site.baseurl}}/img/CS2107-5-8.PNG)


## CA and Trust relationship

Responsibility:
- Verify the info is correct
- Manual checking and thus could be costly


Before certificate issurance, these are checked:
- Domain validation (DV) SSL certificate: Issue if the purchaser can demostrate the right to adminsitratively **manage a domain name**
- Organisation validation (OV) SSL certificate: Issued if purchaser additionally has an organisation actual **existence as a legal entity**
- Extended Validation (EV) SSL Certificate: Issued if the purchaser can persuade the cert provider of its legal identity including **manual verifiacation checks** by a human


#### Types
![CS2107-5-9.PNG]({{site.baseurl}}/img/CS2107-5-9.PNG)


- Root CA: Whose certifcate is self signed
- Subordinate/intermediate CA: Tier 1, 2..
- Leaf CA: Issues the certificate

#### Certification chain

A list of certification 

For each certificate (Except the last one):
- The issuer matches the subject of the next cert in the list
- It is signed by the privqte key of the next certificate in the list
- The last certificate in the list is the root CA

The user should anticpate that the reciever might not have the public key of the certificate given, thus the user should send their public key as well as the public key of the CA.


Diagram and verification:
![CS2107-5-10.PNG]({{site.baseurl}}/img/CS2107-5-10.PNG)
- THe last certificate: The CA serve as the trust anchor
- Each CA refers to the previous
- We need to verify the certificate in the second last in the list and then to the third all the way until we reach the entity

> "The certificate is not trusted because the issue certificate is unknown"
> - This is dangerous, there are many security implications such as malware and bot net etc....
> 
> "Package server certificate verification failed"




#### Certification revocation
- Non expired certificates can be revoked:
	- Private key was compromised
    - Issuing CA was compromised
    - Entity left an organisatiojn
    - Business entity was closed
- A verifier needs to check if a certificate in question is still valid although the certifcate is not expired yet
- Approaches:
	- Certificate revocation list (CRL): CA periodically signs and publishes a revocation list
    - Online certificate status protocol (OCSP): OCSP responder validates a cert in question

Problems:
- Privacy: OCSP responder knows certificarte that you are validating
- Soft failed validation: Some browser proceed in event of no reply to an OCSP request


Solution:
- OSCP stapling: Allows a cert to be accompanied or stabled by a OCSP responder signed by CA
- Part of TLS handshake: CLients do not need to contact CA or OCSP responder
- Drawback: Increased network cost
>  IF we have one million verifiers, there could be a performance issue when OCSP responder response to them. But these verfiers most likely wants to verifies the server cert, thus OCSP does not need to handle verifiers 


# Limitiation/attacks on PKI
- There are alot of CA: Some are malicious
- Rogue CA can forge cert

### Weak browser trust model

Browser trust model:
- Preloaded list of widely used root CAs compiled by web browser developers
- A form of Certificate trust list (CTL) approach, where a list of CA's cert are compiked by a trusted authority


Security issue: 
- Trust anchor: The union of all root CAs
- Which root CA is the one used from the root CA list => As long as there is one root CA that can be use to verify, the browser will use that.
- Certification is only as strong as the weakest root CA


MITM attack by a rouge CA
![CS2107-5-11.PNG]({{site.baseurl}}/img/CS2107-5-11.PNG)
- Mallory pretends to be Alice
- Mallory can see Alice's details

### Null byte injection attack

- Some browser ignores the substring in the entity identity/name but include them when verifiying the certificate
1. The common name in the cert when its being verified: "www.comp.nus.edu.sg\0.hacker.com"
2. The browser displays as "www.comp.nus.edu.sg"
- User thinks they are connecting to the correct website but its not


### Social engineering
- Typosquatting

1. Hacker can register a domain name which looks like another website and obtain the valid certificate of the name
2. Attacker employs a phishing attack tricking a victim to click on this spoof site
3. The address bar correctly displays but the user doesnt notcie that and log in using the victim's credentials

