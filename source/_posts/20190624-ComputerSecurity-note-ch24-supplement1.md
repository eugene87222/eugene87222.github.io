---
title: '[Intro. to Computer Security Course Note] Ch 24 (supplement 1)'
tags:
  - NCTU
  - computer security
  - note
date: 2019-06-24 20:05:53
---

# Ch24 Supplement. Phishing Attacks in Wi-Fi Networks

---

## Goal

- Understand how user credentials can be leaked by a man-in-the-middle phishing attack over Wi-Fi networks
- Expected to learn
   - How to identify a victim's device?
   - How to redirect the victim's traffic to our attack machine?
   - How to steal user credential from intercepted data packets?
   - How to return phishing web pages to the victim?

## Scenario

<img src="https://i.imgur.com/GZvz9VR.png" width="60%"/>

## Four Tasks

- Discover the IP/MAC addresses of a target victim device from a Wi-Fi network
- Redirect all the traffic of the victim device to your attack device
- Redirect the victim device to access a phishing web page
- Launch a man-in-the-middle attack to steal the victim's credential

## Task I

- Discover the IP/MAC addresses of a target victim device from a Wi-Fi network
   - e.g., using "Fing"
- <img src="https://i.imgur.com/kk9vkBb.png" width="60%"/>

### What is ARP (Address Resolution Protocol)

- A communication protocol used for __discovering the link layer (or MAC) address__ associated with a given IP
- A request-response protocol whose messages are encapsulated by a link-layer protocol
- Within the boundaries of a single network, never routed across interworking nodes
- <img src="https://i.imgur.com/eDq4J7V.png" width="60%"/>

## Task II

- Redirect all the traffic of the victim device to your attack device
   - Launch ARP spoofing
   - e.g., using "Arpspoof" (https://github.com/alandau/arpspoof) or "Ettercap"
   - <img src="https://i.imgur.com/b0u0rmh.png" width="60%">
- If the attack is successful
   - the victim's traffic will be routed to the attacker for both uplink and downlink
   - <img src="https://i.imgur.com/BpKmKtI.png" width="60%">

### What is DNS (Domain Name System) Service?

- A hierarchical decentralized naming system for computers, services, or other resources connected to the Internet or a private network
- The resolution of the hierarchical name space is done by a hierarchy of name servers
- Each server is responsible (authoritative) for a contiguous portion of the DNS namespace called a zone
- DNS server answer queries about hosts in its zone
- <img src="https://i.imgur.com/AGg5hXp.png" width="70%">

### DNS Address Resolution

- Domain name resolvers determine the domain name servers responsible for the domain name in question by __a sequence of queries starting with the right-most (top-level) domain label__
- <img src="https://i.imgur.com/iM19Wpx.png" width="60%">

## Task III

- Redirect the victim device to access a phishing web page
   - Launch DNS spoofing
   - e.g., using "Ettercap"
- <img src="https://i.imgur.com/2jADm1I.png" width="60%">
- If the attack is successful
   - An access request to NCTU home page will be redirected to the attack server (140.113.207.243)
   - The attacker can reply with a fake, phishing web page
- <img src="https://i.imgur.com/faWeigz.png" width="60%">

## Task IV

- Launch a man-in-the-middle attack to steal the victim's credential
   - Launch ARP spoofing (but no DNS spoofing)
   - Use "Wireshark" to analyze your intercepted packets
   - Access a web page from the link
- <img src="https://i.imgur.com/4Zglole.png" width="60%">
- If the attack is successful
   - You __can steal user credentials__ from the intercepted packets
- Prerequisite: the web page __cannot be encrypted__
- <img src="https://i.imgur.com/PMubRxS.png" width="60%">