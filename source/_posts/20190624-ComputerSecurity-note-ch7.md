---
title: '[Intro. to Computer Security Course Note] Ch 7'
tags:
  - NCTU
  - computer security
  - note
date: 2019-06-24 19:41:29
description: ' '
---

# Ch7. Denial-of-Service Attacks

DoS is an action that prevents or impairs the authorized use of networks, systems, or applications, by __exhausting resources__ such as central processing units, memory, bandwidth, and disk space

---

# Denial-of-Service Attacks

- Attempts to compromise __availability__ by hindering or blocking completely the provision of some services
- Nowadays: DDoS

## DoS Attacks: Categories of Resources

- Network bandwidth
   - For most org. this is their connections to their Internet Service Provider (ISP)
- System resources
   - Aims to overload or crash the network handling software
- Application resources
   - Involves a number of valid requests, each of which __consumes significant resources__
   - Thus limiting the ability of the server to response to requests from other users

## Classic DoS Attack I

- Ping flooding attack
   - Traffic: ICMP echo request and response packets
   - Goal: __overwhelm the capacity__ of network connection to the target org.
   - Traffic can be handled by higher capacity links on the path, but packets are discarded as capacity decreases
- Two disadvantages from the attacker's perspective
   - Source of the attack is clearly identified
   - Attack reflection at the source system
      - Network performance will be noticeably affected

## Src. Addr. Spoofing

- The use of forged source addr.
   - Usually __via the raw socket interface__ on OS
- Consider the Ping flooding attack
   - Same congestion would result in the router connected to the final, lower capacity link
   - But, ICMP echo response packets would no longer be reflected back
   - Randomly spoofed source addr.: backscatter traffic
- __Make attacking systems harder to be identified__
   - Requiring network engineers to specifically query flow info from routers

## Why Such Easy Forgery of Source Addr. is Allowed

- Development of TCP/IP: generally cooperative, trusting environment
   - Simply does not include the ability to ensure the valid source addr.
- How to address it ?
   - Impose filtering on routers to ensure it
   - As __close to the originating system__ as possible (e.g., borders of the ISP's connection)

## Classic DoS Attack II

- SYN spoofing
   - Goal: attacking the __ability of a network server to respond TCP connection requests__
   - How? Overflowing the tables used to manage such connections
   - Generating a very large number of forged connection requests to the server
   - __Legitimate users are denied access to the server__
- Different from the basic flooding attack
   - Actual volume of SYN traffic can be comparatively low
   - High enough to keep the known TCP connections table filled
- <img src="https://i.imgur.com/Ux7iT2k.png" width="60%"/>

# Flooding Attacks

- Classified based on network protocols
- Intent: __overload the network capacity__
   - Any type of network packets can be used
   - ICMP flood
      - Traditionally network administrators allow such packets into their networks because ping is a useful network diagnostic tool
   - UDP flood
   - TCP SYN flood
      - Total volume of packets is the aim of the attack rather than the system code
- __However, the flooding attacks are limited by a single system__

# Distributed Denial-of-Service Attacks

- Using multiple systems to generate attacks
   - Using malware to subvert(破壞) the system and to install an attack agent, __zombie__
   - Large collections of such systems under the control of one attacker: __botnet__
- Earlier and best-known DDoS tool: Tribe Flood Network(TFN) - Mixter
   - Two-layer command hierarchy
   - Capable: ICMP flood, SYN flood, UDP flood, ICMP amplification
   - Communicate between the handler
- Current DDoS tools
   - Using IRC or HTTP to communicate
   - Hindering analysis of command traffic: agents authentication

# Application-Based Bandwidth Attacks

- Force the target to execute __resource-consuming operations__
- SIP(Session Initiation Protocol) Flood
   - SIP: a protocol for call setup in Voice over IP (VoIP)
      - A text-based protocol with a syntax similar to HTTP
      - Two types: requests and response
- HTTP-based attacks
   - HTTP Flood
   - Slowloris

## SIP INVITE Scenario

- What does the SIP flood attack exploit?
   - A single INVITE request triggers __considerable resource consumption__
   - Two ways
      - Server resources for __processing the INVITE requests__
      - Network capacity is consumed
   - __Legitimate incoming calls are not allowed__
- <img src="https://i.imgur.com/kCFxdBZ.png" width="60%"/>

## HTTP-based Attacks: HTTP Flood

- Bombards Web servers with HTTP requests
- Causing the Web server to
   - Read the file from hard disk
   - Store it in memory
   - Convert it into a packet stream
   - Transmit the packets

## HTTP-based Attacks: Slowloris

- Monopolizing all of the available requests handling threads on the Web server
   - Sending HTTP requests that __never complete__
- Need to understand the HTTP protocol

# Reflector and Amplifier Attacks

- Normal server systems are used as __intermediaries__ for attacks
   - Easier to deploy
   - Harder to trace back to the attacker
- Reflection attacks
- Amplification attacks

## Reflection Attacks

<img src="https://i.imgur.com/NujYhcG.png" width="60%"/>

## Amplification Attacks

- Directing the request to the broadcast address for some network
   - But, TCP services cannot be used for this attack
- Defense: not allow directed broadcasts to routed into a network from outside
- Other defenses:
   - Blocking spoofed src. addr.
   - Limiting network services from being accessed from outside

## DNS Amplification Attacks

- Using packets directed at a legitimate DNS server as the intermediary
- Amplification: small request -> larger response
- Targeting servers that support the __extended DNS features__

# Defenses Against DoS Attacks

<img src="https://i.imgur.com/z8nlErd.png" width="60%"/>

## DoS Attack Prevention: Flooding Attacks

- Block spoofed src. addr.
- Filters may be used to ensure path back to the claimed src. addr.
   - Filters must be applied to traffic, before it leaves ISP's network or at the point of entry to their network
- Imposing limits on the rate of some specific types of packets

## DoS Attack Prevention: SYN Spoofing Attacks

- [SYN cookie](https://zh.wikipedia.org/wiki/SYN_cookie)
   - Cons: https://zh.wikipedia.org/wiki/SYN_cookie#%E7%BC%BA%E9%99%B7
- Selective drop: dropping an entry for an incomplete connection from the TCP connections table when it overflows
- Modifying parameters: table size and timeout period

## DoS Attack Prevention: Others

- Block IP directed broadcast
- Block suspicious services and combinations
- Manage application attacks with a form of graphical puzzle(captcha) to distinguish legitimate human requests
- Use mirrored and replicated servers when high-performance and reliability is required

# Responding to a DoS Attack

- Identify type of attack
- Ask ISP to trace packet flow back to source
- Implement contingency plan
- Update incident response plan
   - Analyze the attack and the response for future handling