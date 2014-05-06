---
layout: post
title: Overview of Key Agreement protocol
---
This is a study notes on key agreement protocols.

# Prerequisite
## Key Agreement Protocol
---------------------------
From [Wikipedia,](http://en.wikipedia.org/wiki/Key-agreement_protocol) 

```
In cryptography, a key-agreement protocol is a protocol
whereby **two or more parties can agree on a key** in such a way that both influence the outcome. If properly done, this **precludes
undesired third-parties from forcing a key choice** on the agreeing parties. Protocols that are useful in practice also **do not 
reveal to any eavesdropping party what key has been agreed upon**.
```

## Diffie-Helman Key Exchange Protocol
---------------------------
1. *Alice* and *Bob* agree upon two prime numbers, *p = 23* and *g = 5*
2. *Alice* chooses a secret integer *a = 6*, then sends Bob *A = g^a mod p*
  * A = 5^6 mod 23
  * A = 15,625 mod 23
  * A = 8
3. *Bob* chooses a secret integer *b = 15*, then sends Alice *B = g^b mod p*
  * B = 5^15 mod 23
  * B = 30,517,578,125 mod 23
  * B = 19
4. *Alice* computes *s = B^a mod p*
  * s = 19^6 mod 23
  * s = 47,045,881 mod 23
  * s = 2
5. *Bob* computes *s = A^b mod p*
  * s = 8^15 mod 23
  * s = 35,184,372,088,832 mod 23
  * s = 2
6. **Alice and Bob** now share a secret **(the number 2)**.

## Man-in-the-middle attack
---------------------------
From [Wikipedia,](http://en.wikipedia.org/wiki/Man-in-the-middle_attack)

The man-in-the-middle attack (often abbreviated MITM, MitM, MIM, MiM, MITMA) in cryptography and computer security is a form of active eavesdropping, in which the attacker,

* makes independent connections with the victims,
* relays messages between them,
* making them believe that they are talking directly to each other over a private connection, 
* when in fact the entire conversation is controlled by the attacker. 

The attacker must be able to 

* intercept all messages going between the two victims and 
* inject new ones, which is straightforward in many circumstances 

A man-in-the-middle attack can succeed only when the attacker can impersonate each endpoint to the satisfaction of the other. It is an attack on mutual authentication (or lack thereof).

**Most cryptographic protocols include some form of endpoint authentication specifically to prevent MITM attacks.**
---------------
Authentication is required to evade MIM attack during key agreement protocol. There are methods as following, 

* Public/private key pairs
* Shared secret keys
* Passwords

### Public keys
Public Keys of the entities are digitally signed by Trusted Certifying Authorities to ensure integrity.

### Passwords
This is based on [Password-authenticated key agreement](http://en.wikipedia.org/wiki/Password-authenticated_key_agreement) and further classified as following.

* Balanced password-authenticated key exchange
* Augmented password-authenticated key exchange
* Password-authenticated key retrieval
* Multi-server methods
* Multi-party methods

## Reference 2
[An efficient protocol for two-party explicit authenticated key agreement | Minghui Zheng, Huihua Zhou andJing Chen](http://onlinelibrary.wiley.com/doi/10.1002/cpe.3198/abstract)

The two-party key agreement protocol can be classified into two categories

* implicit and 
* explicit key authentications. 

This paper investigates the issue on authenticated two-party key agreement protocol over an insecure public network and extends the existing implicit authenticated key agreement protocol into the explicit one by introducing the authenticators.

The advantage of this explicit protocol is that it does not need any fixed public key infrastructure.

Furthermore, this explicit protocol is provably secure in the random oracle under the Computation Gap Diffie-Hellman assumption. 

## Implicit and Explicit Certificates

### Digital certificates : Need and cost
Digital certificates provide mechanism to bind public key with an entity and ensure integrity, along with authenticity of that public key.
Albeit very crucial to have, certificates are substantial investment, both in infrastructure (to protect the keys used), memory (to store and manipulate the certificate), and bandwidth (in repeatedly transferring the certificate to various entities). 

### Implicit or Bullet Certificates

Consider the public-key scheme in an *ad-hoc sensor networks*, which may have frequent new entrants and continually changing trust relationships. 
Implicit certificates provide a *lightweight* certificate scheme for use in these *constrained environments.*
Implicit certificates enable a low-resource trust model for resource-constrained settings, like ad-hoc networks.


In any situation where certificates are generally used and a lightweight certificate is preferable, like e-mail systems, logical and physical access, secure online transactions; and for transactions using mobile devices etc. implicit certificate will come handy.
In these situations, using an implicit certificate provides benefits of Smaller certificates, lower bandwidth usage, optimized processing.


Implicit certificates are made up of three parts.

* Identification data, 
* Public key and 
* Digital signature 


In a conventional certificate, the public key and digital signature are distinct data elements. 
In contrast, the `public key and digital signature are super imposed` in implicit certificates and allow the recipient to extract and verify the public key of the other party from the signature portion. This substantially reduces the bandwidth required as there is no need to transmit both the certificate and the verification key.

# Reference paper: [Overview of Key Agreement Protocols] (http://eprint.iacr.org/2005/289.pdf)
-------------------------------------------------------

### Contents

1. Introduction
  1. Model
  2. Survey on Previous Work
2. Cryptographic Bilinear Maps
3. Two Party Key Agreement
  1. Diffie-Hellman Key Agreement
  2. The MTI Key Agreement
  3. The MQV Key Agreement
  4. Jeong, Katz and Lee’s Key Agreement
4. Two Party ID-Based Key Agreement
  1. Smart’s Key Agreement
  2. Scott’s Key Agreement
  3. Chen and Kudla’s Key Agreement
  4. McCullagh and Barreto’s Key Agreement
5. Three Party Key Agreement
  1. Joux Key Agreement
  2. Zhang, Liu and Kim’s ID-Based Key Agreement
6. Multi Party Key Agreement
  1. Ingemarsson, Tang and Wong’s Group Key Agreement
  2. Burmester and Desmedt Group Key Agreement
  3. Steiner, Tsudik and Waidner’s Group Key Agreement
  4. The Octopus Protocol and The Cube Protocol
  5. Boyd and Nieto’s Group Key Agreement
  6. Bresson and Catalano’s Group Key Agreement
7. Multi Party Dynamic Key Agreement
  1. Bresson, Chevassut and Pointcheval’s Group Key Agreement
  2. Bresson, Chevassut, Essiari and Pointcheval’s Group Key Agreement
  3. Nam, Kim, Kim and Won’s Group Key Agreement
  4. Kim, Lee and Lee’s Group Key Agreement
8. Conclusion


### Gist

1. Introduction

```
  => Efficient key agreement protocols need,
     |- Lower computation,
     |- Communication cost and 
     `- Round complexity
  => Diffie-Hellman Key Exchange Protocol
      |- Basic w/o Authentication.
      `- Authenticated DH
          |- Implicit or Authenticated Key Agreement Protocol [AK]
          `- Explicit or AK with Key Confirmation Protocol [AKC]
  => Basic tools used to authenticate a key agreement
      |- Standard key derivation
      |- Message authentication code (MAC)
      `- Digital signature scheme

  => The first pioneering work for key agreement is the Diffie-Hellman Key Exchange Protocol
  => Basic DH doesnt provide authentication, implying that, MIMA is possible
  ```
  1. Model
  2. Survey on Previous Work
2. Cryptographic Bilinear Maps
3. Two Party Key Agreement
  1. Diffie-Hellman Key Agreement
  2. The MTI Key Agreement
  3. The MQV Key Agreement
  4. Jeong, Katz and Lee’s Key Agreement
4. Two Party ID-Based Key Agreement
  1. Smart’s Key Agreement
  2. Scott’s Key Agreement
  3. Chen and Kudla’s Key Agreement
  4. McCullagh and Barreto’s Key Agreement
5. Three Party Key Agreement
  1. Joux Key Agreement
  2. Zhang, Liu and Kim’s ID-Based Key Agreement
6. Multi Party Key Agreement
  1. Ingemarsson, Tang and Wong’s Group Key Agreement
  2. Burmester and Desmedt Group Key Agreement
  3. Steiner, Tsudik and Waidner’s Group Key Agreement
  4. The Octopus Protocol and The Cube Protocol
  5. Boyd and Nieto’s Group Key Agreement
  6. Bresson and Catalano’s Group Key Agreement
7. Multi Party Dynamic Key Agreement
  1. Bresson, Chevassut and Pointcheval’s Group Key Agreement
  2. Bresson, Chevassut, Essiari and Pointcheval’s Group Key Agreement
  3. Nam, Kim, Kim and Won’s Group Key Agreement
  4. Kim, Lee and Lee’s Group Key Agreement
8. Conclusion



