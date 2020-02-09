---
title: '[Intro. to Computer Security Course Note] Ch 9'
tags:
  - NCTU
  - computer security
  - note
date: 2019-06-24 19:47:14
description: ' '
---

# Ch9. Firewalls and Intrusion Prevention Systems

## The Need for Firewalls

- Internet connectivity is essential
- Why not just equip each workstation / server with strong security features?
   - __Not sufficient; Not cost-effective__
- A single choke point between the protected network and the Internet
   - Complement to host-based security services
   - Imposing security and auditing against Internet-based attacks
   - A single computer systems or a set of two or more systems working together

---

# Firewall Characteristics and access policy

## Firewall Characteristics

- Design goals
   - Only authorized traffic, as defines by the local security policy, will be allowed to pass
   - The firewall itself is immune to penetration

## Firewall Access Policy

- Listing the types of traffic authorized
- Being developed from the org.'s info security risk assessment and policy

## Characteristics for Control Access

- IP addr. and protocol values
   - Used by: packet filter and stateful inspection firewalls
   - Limiting access to specific services
- Application protocol
   - Used by: an app-level gateway
   - Relaying an monitoring the exchange of info for specific app protocols
- User identity
   - Identifying inside users using secure authentication technology, e.g., IPSec
- Network activity
   - Considering time or request, e.g., only in business hours
   - Rate of requests of other activity patterns, e.g., detecting scanning attempts

## Capabilities and Limitations

- Capabilities
   - A single choke point: keeping unauthorized traffic out and simplifying management
   - A location for monitoring
   - A convenient platform for Internet functions, e.g., NAT
   - The platform for IPSec: implementing VPN
- Limitations
   - Cannot protect against attacks bypassing the firewall
   - An improperly secured wireless LAN may be accessed from outside
   - Devices infected outside are attached and used internally

# Types of firewalls

- General model
   - <img src="https://i.imgur.com/4vXYlX3.png" width="60%"/>
- Four major types
   - Packet filtering firewall
   - Stateful inspection firewall
   - Application proxy firewall
   - Circuit-level proxy firewall

## Packet Filtering Firewall

- <img src="https://i.imgur.com/tGZgY8k.png" width="60%"/>
- Applying a set of rules to each incoming and outgoing IP packet
   - Rules based on matches in the IP or TCP header for packets in both directions
   - Matches: determining whether to forward or discard the packet
   - No match: a default action is taken
      - Discard: prohibit unless expressly permitted -> more conservation, __controlled, visible to users__
      - Forward: permit unless expressly prohibited -> easier to manage and use but __less secure__
- Filtering rules are based on info contained in a network packet
   - Src. IP addr.
   - Dest. IP addr.
   - Src. and dest. transport-level addr.
   - IP protocol field
   - Interface
- Example:
   - Allowing inbound and outbound email traffic but to block all other traffic
   - <img src="https://i.imgur.com/dxHEwhG.png" width="60%"/>
   - Problem 1: rule 4 allows external traffic to any dest. port above 1023
   - Problem 2: new rule 4 allows an outside machine to send packets with src. port 23 to internal machines
- Pros
   - Simplicity
   - Transparent to user
   - Fast
- Cons
   - Cannot prevent attacks that employ app specific vulnerabilities or functions
   - Limited logging functionality
   - Don't support advanced user authentication, due to the lack of upper-layer functionality
   - Vulnerable to attacks on TCP/IP protocol issues
   - Susceptible to security breaches caused by improper configurations

## Packet Filtering: Possible Attacks

- IP addr. spoofing
   - src. IP 填 internal host 的 IP
   - Countermeasure: discarding incoming packets with an inside src. addr.
- Src. routing attacks
   - Attacker specifies the route that a packet should take
   - Countermeasure: discarding all packets that just use this option
- Tiny fragment attacks
   - Attacker uses the IP fragmentation option to create extremely small fragments and force the TCP header info into a separate packet fragment
   - Countermeasure: enforcing the first fragment of a packet to contain a predefined minimum amount of the transport header

## Traditional Packet Filtering: Weakness

- Making decisions on an individual packet basis
   - Doesn't take into consideration any higher-layer context
- Must permit inbound network traffic on all the ports (>=1024) for TCP-based traffic
   - Server port: < 1024 (well-known)
   - Client port: 1024 ~ 65536 <- __vulnerability__

## Stateful Inspection Firewall

- <img src="https://i.imgur.com/BAXpYQ1.png" width="60%"/>
- Tightening rules for TCP traffic by creating a directory of outbound TCP connections
   - 狀態檢視防火牆不僅採用封包過濾類似的方法來監控網路傳輸，還會更進一步檢查封包資料流的內容與行為，並非只是單純地過濾個別封包
   - 持續追蹤連接狀態直到結束連線為止，藉以判斷是否為有效的連線而允許封包通過
   - 建立每個連線階段的狀態表，然後根據此前後關聯狀況來判斷是否允許或拒絕此封包通過
- Cons: 無法處理應用層協定

## Application Proxy Firewall

- <img src="https://i.imgur.com/FChl0uN.png" width="60%"/>
- App-level
   - User contacts it using a TCP/IP app
   - Must have proxy codes for specific apps
   - May restrict supported app features
- Pros: more secure than packet filters
- Cons: __additional processing overhead__ on each connection

## Circuit-level Proxy Firewall

- <img src="https://i.imgur.com/4auWNcM.png" width="60%"/>
- Splitting a TCP connection
   - One between itself and a TCP insider
   - One between itself and a TCP outsider
   - Doesn't examine the contents
- Security: determining which connections are allowed
   - Typically used when inside users are trusted
- To reduce the overhead of the app-level proxy firewall
   - Inbound: app-level proxy firewall
   - Outbound: circuit-level proxy firewall

## SOCKS: Circuit-level Gateway

- A framework for client-server apps in TCP/UDP domains to conveniently and securely use the services of a network firewall
   - Client app contacts SOCKS server, authenticates, and sends a relay request
   - SOCKS server evaluate the request
- Three components
   - SOCKS server
   - SOCKS client library
   - SOCKS-ified versions of programs (e.g., FTP, TELNET)

## Firewall Basing

- Stand-alone firewall (basing host)
   - A system identified by the firewall administrator as a critical strong point in the network's security
   - <img src="https://i.imgur.com/KEHfsgO.png" width="60%"/>
      - Running secure OS, only essential services -> a hardened system
   - May require authentication to access proxy or host
   - Each proxy
      - Can restrict features, hosts accessed
      - Small, simple, checked for security
      - Independent, non-privileged
      - Limited disk use, hence __read-only__ code
- Host-based (Server-based) firewall
   - Software modules: used to secure an individual host
      - Available in many OSes
      - Filtering and restricting the flow of packets
      - Common location: a server
   - Pros
      - Filtering rules can be tailored
      - Protection is provided independent of topology
      - Providing an additional layer of protection
         - Used in conjunction with stand-alone firewalls
- Personal firewall
   - Software modules on the personal computers
   - Primary role: to deny unauthorized remote access
      - Can also monitor outgoing activity -> worms and other malware
   - Practice
      - All inbound connections are denied except for those the user explicitly permits
      - Outbound connections are usually allowed

# Firewall location and configurations

## DMZ networks

- DMZ (Demilitarized Zone): a small network isolated from the private network
- Systems located on DMZ networks: externally accessible but need some protections
- <img src="https://i.imgur.com/9sNvWxc.png" width="60%"/>

## Virtual private networks (VPN)

- Containing a set of computers
   - Interconnecting by means of a relatively insecure network
   - Making use of encryption and special protocols to provide security
- Using encryption and authentication in the lower protocol layers to provides a secure connection through an insecure network
   - Most common protocol at the IP level: IPSec (Internet Protocol Security)
- ![](https://i.imgur.com/2iit5Ps.jpg)
- ![](https://i.imgur.com/DKZRSoO.jpg)


## Distributed firewalls

- Local protection: against internal attacks
   - Tailored to specific machines and apps
   - Host-based firewalls on hundreds of servers ans workstation
   - Personal firewalls on local and remote user system
- Global protection: against internal and external attacks
   - Stand-alone firewalls
- <img src="https://i.imgur.com/E3ZQIYt.png" width="60%"/>
- May use both an internal and external DMZ
- External DMZ: __less protection__

## Summary of firewall locations and topologies

- <img src="https://i.imgur.com/B7hAKAO.png" width="60%"/>

# Intrusion prevention systems (IPS)

- Like an IDS
   - Types: Host-based, network-based, distributed/hybrid
   - Approaches: anomaly detection, or signature/heuristic detection

## Host-based IPS (HIPS)

- Alternative solution: sandbox
   - Suited to mobile code
   - Quarantining such code in an isolated system area

## The Role of HIPS

- The main target for hackers and criminals: enterprise point
   - More popular than network devices to be attacked
- Security vendors focus more on the endpoint security products
   - An integrated, single-product suit of functions
- Pros: __various tools work closely together__
   - Easy to manage

## Security Practice: Defense in Depth (DiD)

- A series of defensive mechanisms are layered to protect valuable info
- Using HIPS as one element in a DiD strategy
   - Together with network-level devices

## Network-based IPS (NIPS)

- Inline with NIDS
- Typical methods used by a NIPS device to __identify malicious packets__

## Distributed/Hybrid IPS

- <img src="https://i.imgur.com/6li4RMx.png" width="60%"/>

# Example: Unified Threat Management Product