---
title: '[Intro. to Computer Security Course Note] Ch 2'
tags:
  - NCTU
  - computer security
  - note
date: 2019-06-24 19:26:04
---

# Ch2. Cryptographic Tools

---

# Confidentiality with Symmetric Encryption

## Symmetric Encryption

- Universal technique for providing confidentiality for transmitted of stored data
- __Single-key encryption__

## 2 Requirements

- Strong encryption algo.
- Sender and receiver must have obtained copies of the key in a secure fashion and must keep the key secret

![](https://i.imgur.com/1QCQHqw.jpg)

## Attacking

- Cryptanalytic attacks
    - Rely on<br>1. nature of algo.<br>2. __general characteristics__ of plaintext<br>3. sample plaintext-ciphertext pairs
    - __Exploit the characteristics__ of the algo. to deduce a specific plaintext or key
- Brute-force attacks
    - On average half of all possible keys must be tried to achieve success
    - Knowledge about the expected plaintext!

## Symmetric Block Excryption Algo.

![](https://i.imgur.com/btkbqin.jpg)

- DES Encryption Standard
    - Key length too short
        - 56 bits -> 2^56^ = 7.2 x 10^16^ possible keys (很快就破了)
    - e.g. data encryption algo.
- Triple DES (3DES)
    - Repeats basic DES algo. 3 times using 2 or 3 unique keys<br>(key size: 112 or 168 bits)
    - Key length 比較長
    - Underlying algo. is tje same as DES
    - Drawbacks
        - Not effetient (3 次 DES，瘋子)
        - 64-bit block size -> not effecient / secure
- Advanced Encryption Standard (AES)
    - Widely available in commercial products
    - 128-bit data and 128 / 192 / 256 bit keys

![](https://i.imgur.com/ZQnCJL4.jpg)

## Practical Security Issues

- Symmetric encryption: applied to a unit of data larger than a single 64-bit or 128-bit block<br>e.g., E-mail messages, network packets, database records
- Simplest approach: __electronic codebook (ECB)__
    - Multiple-block encryption
    - Each block of plaintext is encrypted using the same key
    - ![](https://i.imgur.com/ChX8spK.jpg)
- Issue: cryptanalysts may __exploit regularities__ in the plaintext
- How to overcome the weakness of ECB
    - __Cipher Block Chaining (CBC)__
    - ![](https://i.imgur.com/7bQF42O.jpg)

## Block / Stream Ciphers

- Block Cipher
    - Can reuse key
    - More common
    - Usage: file transfer, e-mail, database
- Stream Cipher
    - Faster (XOR), less code
    - Usage: communication

# Meseage Authentication and Hash Function

## 2 Major Aspects

- Message content: not altered
- Message source: authentic

## Another Aspect

- Messafe timeliness / sequence: not artificially delayed or replayed

## Can we use symmetric encryption ?

- Not necessary. content may not need to be encrpyted

## Message Authentication w/o Encrpytion -> __Auth. tag__
    
- Message authentication code (MAC)
    - Use a secret key to generate small block of data
    - Assumption: two communicating parties share the secret key
    - ![](https://i.imgur.com/hRSFsdZ.jpg)
    - Does message authentication really need encrpytion of the message ?
        - __NO!!__
        - 不需要 reversible
        - Only need a way to generate a __tag which can verify message__
- One-way hash function
    - The hash value ensures only unaltered contents. How about authentic source ?

## Hash Function w/ Symmetric Encryption

![](https://i.imgur.com/zV6G66Q.jpg)

## Hash Function w/ Public-key Encryption

![](https://i.imgur.com/ZEUIfRY.jpg)

## Hash Function w/o Encryption: Keyed Hash MAC

![](https://i.imgur.com/poIeWKd.jpg)

## Secure Hash Functions

- Easy to compute
    - Making both hardware and software implementations practical
- One-way (pre-image resistant)
    - For any given code _h_, it is __computationally infeasible__ to find _x_ such that ___H(x) = h___
- Second pre-image (weak collision) resistant
    - __For any given block _x___, it is computationally infeasible to find _y != x_ with _H(y) = H(x)_
- Collision (strong collision) resistant
    - It is computationally infeasible to find __any pair _(x, y)___ such that _H(y) = H(x)_

## Security of Hash Functions

- 2 attack approaches
    - Cryptanalysis<br>exploits logical weaknesses in algo.
    - Brute-force<br>depends solely on the length of the hash code
- Security strength against brute-force attacks
    - Preimage resistant: 2^n^
    - Second preimage resistant: 2^n^
    - Collision resistant: 2^n/2^
- Most widely used hash algo.: Secure Hash Algo. (SHA)
- Applications of hash functions
    - Message authentication
    - Digital signature
    - Passwords
    - Intrusion detection

# Public-Key Encryption

Asymmetric algo.
Based on mathematical functions

## 3 Common Misconceptions about Public-key Encryption

- More secure than symmetric ones
- A general purpose technique that has made symmetric ones obsolete
- Key distribution is trivial

## Requirements for Public-key Cryptosystems

- Computationally easy
    - To create key pairs
    - For sender knowing public key to encrypt messages
    - For receiver knowing private key to decrypt ciphertext
- Computationally infeasible for opponebt knowing public key
    - To determine private key
    - To recover original message which is encrypted by public key

## Encryption Algo. and Applications

![](https://i.imgur.com/bp1McGw.jpg)

- RSA: widely acepted and implemented
- Diffie-Hellman
- Digital Signature Standard: 就只能處理 digital signature
- Elliptic Curve: offer equal security for a far smaller bit size

# Digital Signatures and Key Management

## Digital Signature

## Public-key Certificates: secure distribution of public keys

- Public key distribution
    - Any person can release his / her public key
    - But, anyone can forge such a public announcement
- Solution: public-key certificate
    - Certificate: a public key + a user ID of the key owner
    - The whole block signed by a trusted third party, CA (Certificate Authority)
    - Certificate also includes CA info. and validity period
- X.509 standard
- ![](https://i.imgur.com/TkRsil3.jpg)

## Symmetric Key Exchange using Public-key Encryption: temporary key creation for message encryption

- Diffie-Hellman key exchange
    - No authentication of two communicating partners

## Digital Envelopes: distribution of secret keys

![](https://i.imgur.com/ty5DUpW.jpg)
Can also be used to deliver a symmetric key only

# Random and Pseudorandom Numbers

## 2 Distinct Requirements of Random Numbers

- Randomness
    - Uniform distribution (easy to verify)
    - Independence (difficult to verify)
- Unpredictability