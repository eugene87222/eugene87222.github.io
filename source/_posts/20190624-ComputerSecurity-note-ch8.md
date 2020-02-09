---
title: '[Intro. to Computer Security Course Note] Ch 8'
tags:
  - NCTU
  - computer security
  - note
date: 2019-06-24 19:44:56
description: ' '
---

# Ch8. Intrusion Detection

---

# Intruders

- Cyber criminals
   - Organized crime group with a goal of financial reward
   - Activities: 竊取資料、勒索
   - Meet to trade tips in underground forums
- Activists
   - Outsider attackers
      - Skill level is often low
   - Goals: promote and publicize their social or political causes
   - Activities: 各種攻擊
- State-sponsored org.
   - Groups of hackers sponsored by gov. to conduct espionage(間諜) or sabotage(破壞) activities
   - Known as __APTs__
- Others
   - Hackers with motivations other than the above

## Three Skill Levels of Intruders

- Apprentice
   - Known as "script-kiddies"
- Journeyman
   - Be able to use new vulnerabilities; may be able to locate new ones
- Master

## Intruder Behavior

- Target acquisition and info gathering
   - Identifying and characterizing the target systems using publicly information
   - Using network exploration tools to map target resources
- Initial access
   - Exploiting a remote network vulnerability, guessing weak authentication credentials, or installing malware
- Privilege escalation
- Info gathering or system exploit
- Maintaining access
   - __Install backdoors__
   - Enabling continued access after the initial attack
   - e.g.
      - Modifying or disabling anti-virus programs running on system
- Covering tracks
   - Disabling or editing audit logs to remove evidence of attack activity

# Intrusion detection

## Intrusion Detection System (IDS)

- Three logical components
   - Sensors - collect data
   - Analyzers - determine if intrusion has occurred
   - User interface
- Host-based IDS (HIDS)
- Network-based IDS (NIDS)
- Distributed or hybrid IDS

## Intrusion Detection: Basic Principles

- Another line of defense against intrusions
   - Others: authentication, access control, and firewall
- Based on the assumption: __the behavior of the intruder differs from that of a legitimate user__
- <img src="https://i.imgur.com/8P6HWh5.png" width="60%"/>
- Requirements
   - <img src="https://i.imgur.com/1jMZDGI.png" width="60%"/>

# Analysis approaches

- Anomaly detection
   - Collecting data
      - The behavior of legitimate users over a period of time
   - Analyzing current observed behavior with a high level of confidence
- Signature / Heuristic detection
   - Using a set of __known malicious__ data pattern (signatures) or attack rules (heuristics)
   - __Can only identify known attacks__

## Anomaly detection: Categories

- Statistical
   - __Analysis__ of the observed behaviors / metrics
   - Using univariate, multivariate, or time series models
   - Pros: __simplicity, low computation cost, lack of assumptions about behavior expected__
   - Cons: __difficulty in selecting suitable metrics, not all behaviors can be modeled__
- Knowledge based
   - Classifying the observed data using a set of rules
   - Rules are developed during the training phase, __usually manual__
   - Formal tools: finite-state machine or standard description language
   - Pros: __robustness, flexibility__
   - Cons: __difficulty / time required to develop high quality knowledge rules__
- Machine learning
   - Pros: __flexibility, adaptability, ability to capture interdependencies between factors__
   - Cons: __時間、時間、時間__

## Signature / Heuristic detection

- Signature approaches
   - Widely used in anti-virus products
- Rule-based heuristic identification
   - Identifying known penetrations
   - Identifying suspicious behavior within the bounds of established patterns of usage
   - Specific to the machine and OS

# Host-based intrusion detection

- Main purpose: detect intrusions, log suspicious events, and send alerts
   - Can use either anomaly or signature and heuristic approaches
- Primary benefits: can detect both external and internal intrusions

## Data Sources and Sensors

- System call traces
   - A record of the sequence of system calls by processes on a system
   - Work well for Unix and Linux systems, but problematic on Windows(就你問題最多)
   - 95-99% detection rates
- Audit records
   - Most modern OSes have accounting software that collects info on user activity
   - Pros: __no additional collection software is needed__
   - Cons: may not contain the needed info or in a convenient form
   - 80% detection rates
- File integrity checksums
   - Periodically scan critical files for changes
   - Cons: generate and protect the checksums, __difficult to monitor changing files__
- Registry access
   - Used on Windows to monitor access to the registry

## Anomaly HIDS

- Gathering the system call traces using an OS hook, e.g., BSM (Basic Security Module) audit module
- <img src="https://i.imgur.com/8iqLVMW.png" width="60%"/>
- Using traces of key DDL function calls
- <img src="https://i.imgur.com/LZF69G9.png" width="60%"/>

## Signature of Heuristic HIDS

- Using database of
   - File signatures (patterns of data)
   - Heuristic rules (behavior)
- Widely used in anti-virus software

## Distributed HIDS

- Major issues
   - Need to deal with different data sensors
   - Assure the integrity and confidentiality of the sensor data
   - Architecture
      - Centralized: bottleneck and single point of failure
      - Decentralized: coordination
- <img src="https://i.imgur.com/gmjnQoT.png" width="60%"/>

# Network-based intrusion detection

- Difference between NIDS and HIDS
   - NIDS: 針對網路
   - HIDS: 針對 host 上面 user/software 的行為
- Typically included in the perimeter security infrastructure of an org., located with the firewall
- Including
   - A number of sensors to monitor packer traffic
   - One or more servers for management functions
   - One or more management consoles for the human interface

## Two Types of Network Sensors

- Inline sensors
   - Insert into a network segment
   - Combined with a firewall or a switch
   - Motivation: __block an attack when one is detected__
   - Pros: __no additional separate hardware devices are needed__
   - Cons: negative impact on network performance
- Passive sensors
   - Monitoring a copy of network traffic (the actual traffic doesn't pass through)
   - Pros: __more efficient__, doesn't contribute to packet delay
- <img src="https://i.imgur.com/Voj6A8Z.png" width="60%"/>

## NIDS Sensor Deployment

<img src="https://i.imgur.com/XKd9cMc.png" width="60%"/>

# Distributed or hybrid intrusion detection

- Due to two key problems confronting IDSs
   - These tools __may not recognize new threats__ or modifications of existing threats
   - Difficult to update schemes rapidly enough to deal with threats

# Honeypots

- Decoy systems designed to
   - Lure a potential attacker away from critical systems
   - Collect info about the attacker's activity
   - Encourage the attacker to stay on the system long enough for administrators to respond
- Systems are filled with fabricated info that a legitimate user of the system wouldn't access
- Resources that have no production value
   - Incoming communication is most likely a probe, scan, or attack
   - Initiated outbound communication suggests that the system has probably been compromised

## Honeypot Classifications

- Low interaction honeypot
   - Emulating particular IT services or systems well enough to provide a realistic initial interaction, but does not execute a full version
   - Providing a less realistic target
   - Often sufficient for use as a component of a distributed IDS to warn of imminent attack
- High interaction honeypot
   - A real system, with a full OS, services and applications, which are instrumented and deployed where they can be accessed by attackers
   - Is a more realistic target that may occupy an attacker for an extended period
   - However, it requires significantly more resources
   - If compromised, could be used to initiate attacks on other systems
- <img src="https://i.imgur.com/706SH8j.png" width="60%"/>
