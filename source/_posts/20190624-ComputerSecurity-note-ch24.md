---
title: '[Intro. to Computer Security Course Note] Ch 24'
tags:
  - NCTU
  - computer security
  - note
date: 2019-06-24 19:51:32
description: ' '
---

# Ch24. Wireless Network Security

---

# Wireless Security

- Key factors: contributing to higher security risks (v.s. wired networks)
   - Channel
      - Vulnerabilities in communication protocols
   - Mobility
   - Resources
      - Smartphones/tablets: sophisticated OS but limited memory and processing resources
   - Accessibility
      - Sensors/robots: may be left unattended in remote and/or hostile locations

## Wireless Network Threats

- <img src="https://i.imgur.com/aQb2KPb.png" width="60%"/>

## Wireless Security Measures

- Securing wireless transmissions
   - Principal threats: eavesdropping, altering, inserting, messages, disruption
   - eaves (屋簷)
- Countermeasures for eavesdropping
   - Signal-hiding techniques
   - Encryption
- For altering and inserting
   - Encryption and authentication protocols
- Securing wireless networks
   - Wireless APs: unauthorized access to the network
   - Principal approach: IEEE 802.1X (port-based network access control)
      - Prevent rogue APs and other authorized devices
   - <img src="https://i.imgur.com/snYWqt6.png" width="60%"/>

## Wireless Network Security Techniques

<img src="https://i.imgur.com/M4Dkdlb.png" width="60%"/>

# Mobile Device Security

- An organization's networks must accommodate
   - Growing use of new devices
   - __Cloud-based apps__
   - De-perimeterization
      - A multitude of network perimeters around devices, apps, user, and data
   - External business requirements

## Security Threats

- <img src="https://i.imgur.com/10rJp5U.png" width="60%"/>

## Mobile Device Security Strategy

- Device security
- Traffic security
   - Based on encryption and authentication
   - via VPN
- Barrier security
   - Firewall
- <img src="https://i.imgur.com/veezYlX.png" width="60%"/>

# IEEE 802.11 Wireless LAN Overview

## Terminology & Services

- Access point (AP)
   - Any entity that has station functionality and provides access to the distribution system via the wireless medium for associated stations
- Basic service set (BSS)
   - A set of stations controlled by a single coordination function
- Coordination function
   - The logical function that determines when a station operating within a BSS is permitted to transmit and may be able to receive PDUs
- Distribution system (DS)
   - A system used to interconnect a set of BSSs and integrated LANs to create an ESS
- Extended service set (ESS)
   - A set of one or more interconnected BSSs and integrated LANs that appear as a single BSS to the LLC layer at any station associated with one of these BSS
   - <img src="https://i.imgur.com/pZpfprh.png" width="60%"/>
- MAC protocol data unit (MPDU)
   - __The unit of data__ exchanged between two peer MAC entities using the services of the physical layer
- MAC service data unit (MSDU)
   - __Information__ that is delivered as a unit between MAC users
- Station
   - Any device that contains an IEEE 802.11 conferment MAC and physical layer
- <img src="https://i.imgur.com/iF0ugu7.png" width="60%"/>

## Distribution of Messages within a DS

- Two services involved
   - Distribution: __exchange__ MPDUs between two BSS
   - Integration: data __transfer__ between a Wi-Fi station and a LAN station on an integrated IEEE 802x LAN

## Association-Related Services

- Transition types, based on mobility:
   - No transition
   - BSS transition
      - ![](https://i.imgur.com/sMcBV7H.jpg)
   - ESS transition
      - ![](https://i.imgur.com/1bZ6slq.jpg)

## Distribution Service

- Association
   - Establishes an initial association between a station and an AP
- Reassociation
   - Enables an established association to be transferred from one AP to another
- Disassociation

## Wireless Fidelity (Wi-Fi) Alliance

- 802.11b
   - First 802.11 standard to gain broad industry acceptance
- Wireless Ethernet Compatibility Alliance (WECA)
   - Industry consortium(合夥) formed in 1999: interoperation between vendors
- Term used for certified 802.11b products: Wi-Fi
- Wi-Fi Protected Access (WPA)
   - Certification procedures for IEEE 802.11 security standards
   - Most recent version: WPA2

## IEEE 802.11 Protocol Stack

<img src="https://i.imgur.com/W99PYik.png" width="60%"/>

## General IEEE 802 MPDU Format

<img src="https://i.imgur.com/J7C1ZFj.png" width="60%"/>

# IEEE 802.11i Wireless LAN Overview

- Wired Equivalent Privacy (WEP) algorithm
   - 802.11 privacy
- Wi-Fi Protected Access (WPA)
   - Set of security mechanisms: eliminates most 802.11 security issues
   - Based in the current state of the 802.11i standard
- Robust Security Network (RSN)
   - <img src="https://i.imgur.com/CO4gSdy.png" width="60%"/>
   - <img src="https://i.imgur.com/grye5ly.png" width="60%"/>
- Wi-Fi Alliance certifies vendors in compliance with the full 802.11i (WPA2)

## Five Phases of Operation for an RSN

- <img src="https://i.imgur.com/DC85X70.png" width="60%"/>
- Phase 1: Discovery Phase
   - Security capabilities
      - Confidentiality and MPDU integrity protocols
      - Authentication method
      - Cryptography key management approach
   - Cipher suite (Confidentiality/Integrity)
      - WEP, TKIP, CCMP
   - AKM: Authentication and Key Management
      - IEEE 802.11x, pre-shared key
   - <img src="https://i.imgur.com/eMsu6xU.png" width="60%"/>
   - 802.1X Access Control
      - <img src="https://i.imgur.com/3DRfr6p.png" width="60%"/>
- Phase 2: Authentication Phase
   - IEEE 802.11x AC
      - 802.1X Control channel is unblocked
      - 802.11 data channel is blocked
   - Three phases
      - Connect to AS
      - EAP exchange
      - Secure key delivery
   - <img src="https://i.imgur.com/DGzgnYn.png" width="60%"/>
   - EAP Authentication Protocol
      - Initiated by the server (authenticator)
      - Authentication is mutual between the client and authentication server
      - <img src="https://i.imgur.com/a72D2Os.png" width="60%"/>
   - Popular EAP Methods
      - Cisco LEAP (Lightweight EAP)
         - __complex passwords are required__
      - EAP-FAST (EAP-Flexible Authentication via Secure Tunneling)
         - __No need of strong password or any certificate__
         - Using a PAC (Protected Access Credential) to establish a TLS tunnel
      - EAP-TLS
         - Using PKI: both client and AS need a certificate (X509 certificates)
         - __One of the most secure EAP standards available__
      - PEAP (Protected EAP)
         - Encapsulating EAP within a potentially __encrypted and authenticated TLS tunnel__
         - Only the server authentication is performed using PKI certificate
         - Client is authenticated using either __EAP-GTC__ or __EAP-MSCHAPv2__ within the tunnel
            - EAP-GTC (Generic Token Card)
            - EAP-MSCHAPv2 (Microsoft's Challenge Handshake Authentication Protocol)
         - <img src="https://i.imgur.com/iFSalIT.png" width="60%"/>
- Phase 3: Key Management Phase
   - Pairwise keys: for communication between a STA and an AP
      - Pre-shared key (PSK)
      - Master session key (MSK)
      - Pairwise master key (PMK)
         - PSK or derived from MSK
      - Pairwise transient key (PTK)
      - Hierarchy
         - <img src="https://i.imgur.com/ZQP8XmI.png" width="60%"/>
   - Group keys: for multicast communication
      - Group master key (GMK)
      - Group temporal key (GTK)
      - Hierarchy
         - <img src="https://i.imgur.com/kgkCdCe.png" width="60%"/>
   - IEEE 802.11i Phases of Operation
      - 4-way Handshake
         - <img src="https://i.imgur.com/2Jdydjt.png" width="60%"/>
      - Group Key Handshake
         - <img src="https://i.imgur.com/RvAPxOY.png" width="60%"/>
- Phase 4: Protected Data Transfer Phase
   - Temporal Key Integrity Protocol (TKIP)
      - Only software changes are required to old WEP
      - Message integrity
         - Message Integrity Code (MIC)
         - 64-bit: source/destination MAC address + data filed + key material
      - Data confidentiality
         - Encrypting MPDU + MIC using RC4
      - 256-bit TK
         - Two 64-bit keys for MIC: one key for each direction
         - 128 bits: generate the RC4 key for encryption
         - TKIP sequence counter (TSC): monotonically increasing
            - Included with each MPCU and protected by MIC -> __against replay attack__
            - Combined with session TK -> dynamic encryption key
   - Counter Mode-CBC MAC Protocol (CCMP)
      - 需要硬體支援
      - Message integrity
         - Cipher block chaining message authentication code
      - Data confidentiality
         - CTR block cipher mode of operation with __AES__
      - Same 128-bit AES key for both
      - A 48-bit packet number: __a nonce(暫時) to prevent replay attack__
   - IEEE 802.11i Pseudorandom Function (PRF)
      - A pseudorandom bit stream: HMAC-SHA-1
         - A message and a key (at least 160 bits) -> 160-bit hash value
         - SHA-1 property: change of a single bit -> a new hash value with no apparent connect
         - <img src="https://i.imgur.com/k4Mkwzd.png" width="60%"/>
         - PTK:
            - K = PMK
            - A = "Pairwise key expansion"
            - B = Concatenation of two MAC address and two nonces
            - Len = 384 bits
