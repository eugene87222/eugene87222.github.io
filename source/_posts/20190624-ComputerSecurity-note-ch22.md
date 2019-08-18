---
title: '[Intro. to Computer Security Course Note] Ch 22'
tags:
  - NCTU
  - computer security
  - note
date: 2019-06-24 19:58:16
---

# Ch22. Internet Security Protocols and Standards

---

# Secure E-mail

<table style="">
    <tr>
        <th style="font-weight: normal;">MIME</th>
        <th style="font-weight: normal;">S/MIME</th>
    </tr>
    <tr>
        <th style="font-weight: lighter;">Extension to the old RFC 822 specification of an Internet mail format<br>- RFC 822 defines a simple heading with To, From, Subject<br>- Assu,es ASCII text format</th>
        <th style="font-weight: lighter;">Secure/Multipurpose Internet Mail Extension<br>Based on RSA<br>Provides the ability to sign and/or encrypt e-mail messages</th>
    </tr>
    <tr>
        <th style="font-weight: lighter;"><img src="https://i.imgur.com/o9mUChP.png" width="60%"/></th>
        <th style="font-weight: lighter;"><img src="https://i.imgur.com/aCLJAAC.png" width="60%"/></th>
    </tr>
</table>

## Typical S/MIME Process for Creating an S/MIME Message

<img src="https://i.imgur.com/fB0mxph.png" width="60%"/>

## S/MIME Functions

- Enveloped data
   - Encrypted content and associated keys
- Signed data
   - Encoded message + signed digest
- Clear-signed data
   - Cleartext message + signed digest
- Signed and enveloped data
   - Nesting of signed and encrypted entities

## Enveloped Data Using Public-key Infrastructure

- M -> 3DES(M) -> X + 3DES(M) -> ELGamal(X + 3DES(M))
   - M: message
   - X: a session encryption key
   - User recipient's ELGamal's public key to encrypt X + 3DES(M)
   - ELGamal is based no the Diffie-Hellman public-key exchange algorithm
- __Radix-64__ is used to convert the ciphertext to ACSII format
- Basic tool that permits widespread use of S/MIME is the __public-key certificate__
- S/MIMNE uses certificates that conform to the international standard X.509.3

## Signed and Clear-signed Data

- Signed data -> Base64(content + sig)
- Clear-signed data -> content + Base674(sig)
- DSS(SHA-1(MEssage), DSS-private-key)
- RSA(SHA-1/MD5(Message), RSA-private-key)
- __Radix-64 or Base64__ mapping is used to map the signature and message into printable ASCII characters

# DomainKeys Identified Mail (DKIM)

- A specification of cryptographically signing e-mail messages
- A proposed Internet standard

## Internet Mail Architecture

- User world: MUA
- Transfer world: MHS
   - Composed of MTAs
- <img src="https://i.imgur.com/QGcBAS8.png" width="60%"/>

## Why DKIM

- An email authentication technique that is transparent to the end user
- Reasons
   - S/MIME depends on both the sending and receiving users employing S/MIME
      - But, the bulk of incoming mail does not use S/MIME
      - __S/MIME signs only the message content__
         - Header information concerning origin can be compromised
      - Applied to all mail from cooperating domains
      - __Preventing forgers from masquerading as good senders__

## Simple Example of DKIM Deployment

- DNS = domain name system
- MDA = mail delivery agent
- MSA = mail submission agent
- MTA = message transfer agent
- MUA = message user agent
<img src="https://i.imgur.com/JX8yM8c.png" width="60%"/>

# Secure Sockets Layer (SSL) and Transport Layer Security (TLS)

- Secure Socket Layer (SSL)
   - One of the most widely used security services
- Transport Layer Security (TLS)
   - Becoming Internet standard RFC4346
   - General-purpose service: as a set of protocols that rely on TCP
   - Two implementation choices
      - As part of the underlying protocol suite: transparent to apps
      - Be embedded in specific packages: e.g., most browsers come equipped with SSL

## SSL/TLS Protocol Stack

- <img src="https://i.imgur.com/cV2D1ER.png" width="60%"/>

## TLS Concepts

- TLS Connection
   - A transport (in the OSI layering model definition) that provides a suitable type of service
   - Peer-to-peer relationships
   - Transient (暫時的)
   - Every connection is associated with one session
- TLS Session
   - An association between a client and a server
   - Created by the __handshake protocol__
   - __Define a set of cryptographic security parameters__
   - Used to avoid the expensive negotiation of new security parameters for each connection

## TLS Record Protocol Operation

- <img src="https://i.imgur.com/tsZPibK.png" width="60%"/>

## Handshake Protocol

- TLS 最複雜的部份
- __Is used before any application data are transmitted__
- Authenticate each other -> Negotiate encryption and MAC algorithms -> Negotiate cyrptographic keys to be used
- Exchanges has four phases

## Handshake Protocol Action 1 (phase 1 & 2)

<img src="https://i.imgur.com/zgyfypi.png" width="60%"/>

## Handshake Protocol Action 2 (phase 3 & 4)

<img src="https://i.imgur.com/Nfv18KU.png" width="60%"/>

## ClientHello (RFC)

```c
struct {
   ProtocolVersion client_version;
   Random random;
   SessionID session_id;
   CipherSuite cipher_suites <2..2^16-2>;
   CompressionMethod compression_methods <1..2^8-1>;
} ClientHello;
```

## ServerHello (RFC)

```c
struct {
   ProtocolVersion server_version;
   Random random;
   SessionID session_id;
   CipherSuite cipher_suite;
   CompressionMethod compression_method;
} ServerHello;
```

## Four TLS specific protocols

- Change Cipher Spec Protocol
   - One of four TLS specific protocols that use the TLS Record Protocol
   - Simplest
   - Consists of a single message which consists of a single byte with the value 1
   - Sole purpose of this message is to __cause pending state to be copied into the current state__
   - Hence updating the cipher suite in use
- Alert Protocol
   - Two bytes
      - 1^st^ byte: warning (1), fatal (2)
         - For fatal, TLS implementation __terminates__ the TLS connection
         - For other TLS connections using the same TSL session, they may continue, __but no new TLS connections may be established__
      - 2^nd^: specific alert code (RFC5246-appendix)
         - close_notify(0), unexpected_message(10), etc
- Heartbeat Protocol
   - A periodic signal generated to indicate normal operation or to synchronize other parts of a system
   - Typically used to __monitor the availability of a protocol entity__
   - Runs on top of the TLS Record Protocol
   - Established during __phase 1__ of the handshake protocol
   - Each peer indicated whether it supports heartbeats
   - Serves two purposes:
   - __Assures the sender that the recipient is still alive__
   - Generates activity across the connection __during idle periods__

## SSL/TLS Attacks

<img src="https://i.imgur.com/fHCcQVE.png" width="60%"/>

## The Heartbleed Exploit (Source: BAE Systems)

<img src="https://i.imgur.com/SAQRWwv.png" width="60%"/>

# HTTPS (HTTP over SSL/TLS)

- Secure communication between a Web browser and a Web server
- Build into all modern Web browsers
   - Search engines do not support HTTPS
- Connection initiation and closure
   - HTTP client act as TLS client
   - TLS handshake -> HTTP request
   - Three levels: HTTP, TLS session, TCP

## IPSec v.s. SSL/TLS

<img src="https://i.imgur.com/NLQtElg.png" width="60%"/>

## Applications of IPSec

- Secure branch office connectivity over the Internet
- Secure remote access over the Internet
- Establishing extranet and internet connectivity with partners
- Enhancing electronic commerce security

## Benefits of IPSec

- Strong security
- Resistant to bypass at a firewall
- Transparent to apps
   - No need to change software
- Transparent  to end user
   - No need to train users on security mechanisms
- Routing apps: prevent attackers from disrupting communications or diverting some traffic
   - A router advertisement from an authorized router
   - A neighbor advertisement from an authorized router
   - A redirect message from the router to which the initial packet was sent
   - A routing update is nor forged
- The Scope of IPSec
   - Two main functions
      - Encapsulating Security Payload (ESP): a combined authentication/encryption function
      - A key exchange function
   - VPN: both authentication and encryption are generally desired
   - Authentication Header (AH): authentication-only function (deprecated)

## Security Associations

- A key concept of IPSec
   - One-way relationship between a sender and a receiver
   - Two-way secure exchange: two SAs are required
- Uniquely identified by three parameters
   - Security parameter index (SPI)
   - IP destination address
   - Protocol identifier: AH or ESP
- Characterized by the following parameters
   - Sequence number counter: 32-bit
   - Sequence counter overflow: A flag -> whether overflow -> an auditable event
   - Antireplay window: defining a sliding window
   - AH information
      - Algorithm, keys, key lifetimes
   - ESP information
      - Algorithm, keys, init values, key lifetimes
   - Lifetime of this security association
   - IPSec protocol mode: tunnel or transport
   - Path MTU

## Two IPSec Operation Modes

- Transport and tunnel modes
- <img src="https://i.imgur.com/dPmSPN6.png" width="60%"/>
- <table style="">
    <tr>
        <th style="font-weight: normal;">Transport Mode</th>
        <th style="font-weight: normal;">Tunnel Mode</th>
    </tr>
    <tr>
        <th style="font-weight: lighter;">Provides protection to the payload of an IP packet<br>Typically used for end-to-end communication __between two hosts__<br>ESP protects the __IP payload__ but not the IP header</th>
        <th style="font-weight: lighter;">Provides protection to the __entire IP packet__<br>Entire original packet travels through a tunnel from one point to another<br>Used when one or both ends of a security association are a security gateway<br>Hosts on networks behind firewalls may engage in secure communications without implementing IPSec</th>
    </tr>
</table>

## Encapsulating Security Payload

- Providing authentication and confidentiality services
- <img src="https://i.imgur.com/xzPy2dV.png" width="60%"/>

## IPSec: AH + ESP

- IP AH only
   - <img src="https://i.imgur.com/gih8yFX.png" width="60%"/>
- IP AH + ESP
   - Transport mode
      - <img src="https://i.imgur.com/KJw67Ky.png" width="60%"/>
   - Tunnel mode
      - <img src="https://i.imgur.com/xmR09TT.png" width="60%"/>

# IPv4 and IPv6 Security