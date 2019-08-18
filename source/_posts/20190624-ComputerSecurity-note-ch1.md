---
title: '[Intro. to Computer Security Course Note] Ch 1'
tags:
  - NCTU
  - computer security
  - note
date: 2019-06-24 19:10:38
---

# Ch1. Overview

---

# 3 Key

## Confidentiality

Assure that private or confidential info is not disclosed to unauthorized individuals
Privacy: Assure that individuals control or influence what info related to them may be collectd and stored

## Integrity

Data integrity: info are __changed only in a specified / authorized manner__
System integrity: system performs well in an unimpaired manner

## Availability

Assure that system works promptly and service is not denied to authorized users

# Other 2

## Authenticity

Property is genuine and able to be verified and trusted

## Accountability

Requirement for actions of an entity to __be traced__ uniquely to that entity

# Model of Computer Security

## Vulnerability

Weakness
- Corrupt: loss of integrity
- Leaky: loss of confidentiality
- Unavailability or very slow

Threat
__Capable of exploiting vulnerability__

Attack
- Passive: make use of info, but doesn't affect system resources
- Active: alter system resources
- Inside: by an authorized user (using in a way not approved)
- Outside: by an unauthorized user

Countermeasures

# Security Concepts / Relationships

![](https://i.imgur.com/ff0Bwch.jpg)

# Threats / Attacks

<table style="">
    <tr>
        <th style="font-weight: normal;">Threat Consequence</th>
        <th style="font-weight: normal;">Threat Action (Attack)</th>
    </tr>
    <tr>
        <th style="font-weight: lighter;">Unauthorized Disclosure<br>- threats to confidnentiality</th>
        <th style="font-weight: lighter;">1. Explosure<br>2. Interception<br>3. Inference (推斷)<br>4. Intrusion</th>
    </tr>
    <tr>
        <th style="font-weight: lighter;">Deception<br>- threats to integrity</th>
        <th style="font-weight: lighter;">1. Masquerade<br>2. Falsification<br>3. Repudiation (否認)</th>
    </tr>
    <tr>
        <th style="font-weight: lighter;">Disruption<br>- threats to availability / system integrity</th>
        <th style="font-weight: lighter;">1. Incapacitation<br>2. Corruption: alters system operation<br>3. Obstruction</th>
    </tr>
    <tr>
        <th style="font-weight: lighter;">Usurpation (篡奪)<br>- threats to system integrity</th>
        <th style="font-weight: lighter;">1. Misappropriation<br>2. Misuse</th>
    </tr>
</table>

# Security Functional Requirements

## Technical Measures

## Management Controls / Procedures

## Overlapping Technical / Management

# [Fundamental Security Design ](http://www.informit.com/articles/article.aspx?p=30487&seqNum=2)

## Economy of Mechanisnm

Design should be as simple as possible

## Fail-safe Defaults

Access decisions should be based on permission rather than exclusion

## Complete Mediation

Every access must be check against the access control mechanism

## Open Design

就把設計公開

## Separation of Privilege

大家的權限不一樣

## Least Privilege

## Least Common Mechanism

## Psychological Acceptability

Should not interfere unduly with the work of users or hinder the usability or accessibility of resources

## Isolation

## Encapsulation

A specific form of isolation based on object-oriented functionality

## Modularity

就包成 module

## Layering

Use of multiple,  overlapping protection approaches

## Least Astonishment

# Attack Surfaces

![](https://i.imgur.com/EgglfHs.jpg)
Make developers aware of where security mechanisms are required

# Attack Trees

- Root: the attack goal
- Leaf: different ways to initial an attack
- Each node (other than a leaf): AND / OR node

Why ?

- Effectively exploit the info available on attack pattern
- Document security attacks in a structured form that reveals key vulnerabilities
- Can know how to design system / coutnermeasures

# Computer Security Strategy

## 3 Aspects

- Specification / policy: what is the security scheme supposed to do ?
- Implementation / mechanisms: how to ?
- Correctness / assurance: does it work ?

## Security Policy

- A formal statement of rules and practices
- A security manager needs to consider
    - __value__ of assets being protected
    - __vulnerabilities__ of the system
    - __potential threats__ and the likehood of attacks
    - trade-off: ease of use v.s. security
    - trade-off: cost of security v.s. cost of failure and recovery

## Security Implementation / Assurance