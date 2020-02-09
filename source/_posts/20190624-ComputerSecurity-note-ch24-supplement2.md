---
title: '[Intro. to Computer Security Course Note] Ch 24 (supplement 2)'
tags:
  - NCTU
  - computer security
  - note
date: 2019-06-24 20:06:14
description: ' '
---

# Ch24 Supplement. Cellular Network Security

---

# Evolution of mobile networks

<img src="https://i.imgur.com/whI84Ny.png" width="60%"/>

## Standards Body for Mobile Network: 3GPP

- An international standards body
- Evolves and standardizes GSM, UMTS, LTE, among others
- We will primarily discuss 3GPP standards

## Current Mobile Networks

<img src="https://i.imgur.com/aJ3Du9S.png" width="60%"/>

## Technology: 3G -> 4G

- 4G LTE: First global standard for mobile broadband
   - More data capacity
   - Faster speed
   - Lower latency
   - New service paradigm
- Key enabler: network architecture evolution

## Network Architecture Evolution

<img src="https://i.imgur.com/JmLnWwL.png" width="60%"/>

## 2G is based on Circuit Switching (CS)

- End-end resources reserved for "call"sss
   - No sharing
- <img src="https://i.imgur.com/OnqbP2F.png" width="40%"/>

## CS Signaling

- Used to setup, maintain, and tear down VC
- Used in 2G, 3G
- <img src="https://i.imgur.com/KyJ9lg6.png" width="60%"/>

## Packet Switching (PS)

- Store-and-forward at intermediate routers
- Used by the Internet
- <img src="https://i.imgur.com/rUMl9m1.png" width="60%"/>

## PS Signaling

- No call setup at network layer
- No network-level concept of "connection"
- Packets forwarded using destination host address
   - Packets between same source-destination pair may take different paths
- <img src="https://i.imgur.com/A6fFWKL.png" width="60%"/>

## 4G Cellular Network Architecture

<img src="https://i.imgur.com/KRQzUKl.png" width="60%"/>
- MME: Mobility Management Entity
- BS: Base Station

## 3G/4G Network Architecture

<img src="https://i.imgur.com/sgjzdV1.png" width="60%"/>

## Operations

- Two main planes in operation in parallel
   - Data/User plane: content delivery
   - Control plane: signaling functions
      - Three Major Functions
         - Radio Resource Control (RRC)
         - Mobility Management (MM)
         - Connection Management (CM)
         - <img src="https://i.imgur.com/0Wp6USa.png" width="60%"/>
- Additional plane that woks with the above
   - Management plane: configurations, monitoring

# How to set up data services in 4G networks

<img src="https://i.imgur.com/9m2gWVp.png" width="60%"/>

# Security in 4G networks

<img src="https://i.imgur.com/spnq6Pa.png" width="60%"/>
<img src="https://i.imgur.com/XpOMLQX.png" width="60%"/>
<img src="https://i.imgur.com/AdDMcjy.png" width="60%"/>
- IMSI (International Mobile Subscriber Identity): 國際移動用戶識別碼
- TMSI (Temporary Mobile Subscriber Identity): 臨時移動用戶識別碼
- <img src="https://i.imgur.com/CJT2fK8.png" width="60%"/>
<img src="https://i.imgur.com/aoJlTKS.png" width="60%"/>