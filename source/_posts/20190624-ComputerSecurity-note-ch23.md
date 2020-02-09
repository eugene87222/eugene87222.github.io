---
title: '[Intro. to Computer Security Course Note] Ch 23'
tags:
  - NCTU
  - computer security
  - note
date: 2019-06-24 20:02:05
description: ' '
---

# Ch23. Internet Authentication Applications

---

# Kerberos

- A software utility available both in the public domain and in commercially supported versions
- The defacto standard for remote authentication
- A trusted third party authentication service
   - Clients and servers trust Kerberos to mediate their mutual authentication
   - Requires that
      - A user proves his or her identity for each service invoked
      - Optionally, services prove their identity to clients

## Security Issues between Clients and Servers?

- In an unprotected network environment, any client can apply to any server for server
- Obvious security risk?
   - Impersonation: an opponent can __pretend to be another client__ and obtain unauthorized privileges on server machines
- Countermeasure
   - Confirm the identities of clients
- Alternative: using an __authentication server (AS)__
   - Once the AS has verified the user's identity, it can pass this information on to an application server

## Kerberos Overview

- AS shares a unique secret key with each server
- Session key: one-time encryption key
- Ticket and session key are both encrypted using the user's password as the encryption key
- Password is never passed over the network
- ![](https://i.imgur.com/uhVkfXL.jpg)
   1. User logs on to workstation and requests service on host
   2. AS verifies user's access right in database, creates ticket-granting ticket and section key. Results are encrypted using key derived from user's password
   3. Workstation prompts user for password to decrypt incoming message, then send ticket and authenticator that contains user's name, network address and time to TGS
   4. TGS decrypts ticket and authenticator, verifies requests then creates ticket for requested application server
   5. Workstation sends ticket and authenticator to host
   6. Host verifies that ticket and authenticator match, then grants access to service. If mutual authentication is required, server returns an authenticator
- Ticket: a set of credentials
   - User's ID, server's ID, timestamp, lifetime
- Entire ticket is encrypted using a secret DES key shared by the AS and the server
- Why TGS?
   - Query the user for his password for each service
      - Inconvenient
   - Store the password in memory for the duration of the logon session
      - 有安全風險
- TGS: a ticket to get more ticket
- How to counter the following threats for ticket-granting ticket?
   - Ticket may be stolen and reused
      - Timestamp
   - Alteration of the ticket
      - Encrypted with a secret key __known only to the AS and TGS__
   - User spoofing
      - Authentication based on the encryption with the user's password
   - Reply attack
      - Authenticator, which is not reusable

## Kerberos Realms

- A Kerberos realm: full-service Kerberos environment
   - A Kerberos server
   - A number of clients
      - Each registers with the Kerberos server; the __server holds a database__ for the user ID/password
   - A number of app servers
      - Each registers with the Kerberos server __and shares a secret key__ with it

## Interrealm Authentication

- 不同 realm 的 Kerberos server 彼此 shares a secret key
- Kerberos servers are registered with each other

## Kerberos Version 4 & 5

- 4: most widely used in late 1980s
- 5:
   - Introduced in 1993, updated in 2005
   - AES is the default choice (DES in v4)
   - Authentication forwarding
      - Enabling a client to access a server and have that server access another server on behalf of the client

## Performance Issues

- Very little performance impact in a large-scale environment
   - If the system is properly configured
   - The amount of traffic needed for the granting ticket: modest
- Does it require a dedicated platform?
   - Not wise to run it on the same machine as a resource-intensive app
   - Its security is best assured by placing it on a __separate, isolated machine__
- How about using multiple realms to maintain performance?
   - Probably not
   - The motivation of multiple realms is administrative

# X.509

## X.509: Public-key Certificate

- A certificate
   - Linking a public key with the identity of the key's owner
   - The whole block signed by a trusted third party
- Third party: certificate authority (CA)
- User can present his public key to the authority in a secure manner ad obtain a certificate
- <img src="https://i.imgur.com/wTwLgCn.png" width="60%"/>

## X.509

- A certificate revocation list (CRL)
   - Signed by the issuer
   - Containing a serial number of a certificate and the revocation date
- When receiving a certificate, an app should determine whether it has been revoked
   - Check CRL
   - Very few apps do this due to __high overheads__
- A lightweight protocol for the revocation in RFC 6960
- Hash signature
   - Using __SHA-2, SHA-2__ now

# Public-Key Infrastructure (PKI)

- RFC 4949: the set of hardware, software, people, policies, and procedures needed to create, manage, store, distribute, and revoke digital certificates __based on asymmetric cryptography__
- <img src="https://i.imgur.com/dUmMB13.png" width="60%"/>

## CA in Trust Store

- Either directly sign "end-user" certificates
- Or sign a small number of "Intermediate-CAs"
- All the hierarchy are very small, and all are equally trusted

## Issues with the PKI Model

- Issue 1: reliance on the user to make an informed decision when there is a problem verifying a certificate
- Issue 2: assuming that all of the CAs in the "trust store" are equally trusted, equally well managed, and apply equivalent policies
- Issue 3: different implementations, in the various web browsers and OS, use different "trust stores"
   - Present different security views to users

## Improve the X.509 Certificates

- Recognize that many apps do not require formal linking of a public key to a verified identity
- Improvement 1: confirming continuity in time
   - Apps keep a record of certificate details for all sites they visit
- Improvement 2: confirming continuity in space
   - Using a number of widely separated "network notary(公證人) servers" that keep records of certificates for all sites they view