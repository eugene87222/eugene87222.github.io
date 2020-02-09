---
title: '[Intro. to Computer Security Course Note] Ch 5'
tags:
  - NCTU
  - computer security
  - note
date: 2019-06-24 19:37:38
description: ' '
---

# Ch5. Database and Cloud Security

---

# Database Management Systems

## DBMS Architecture

- DDL(data definition language): defines the database logical structure and procedural properties
- DML(data manipulation language): provides a powerful set of tools for app developers

![](https://i.imgur.com/9A8RekB.jpg)

# Relational Databases

- Constructed from tables of data
- Have multiple tables linked by identifiers
- Use a query language to access data items meeting specified criteria

## Relational Database Elements

- Relation / table / file
- Tuple / row / record
- Attribute / column / field
- View / virtual table: result of a query

## Structured Query Language (SQL)

Originally developed by IBM in the mid-1970s

# SQL Injection Attacks

## Injection Technique

- Typical SQLi attacks: permaturely terminating a text string and appending a new command
    - comment mark `--`

## 3 Categories of SQLi Attacks

- In-band attacks
    - Tautology (e.g., `' OR '1'=='1'`)
    - End-of-line comment (e.g., `--`)
    - Piggybacked queries
        - The attacker adds additional queries beyond the intended query
- Out-of-band attacks
    - Data are retrieved using a different channel, e.g., email instead of web pages
    - Used when there are limitations on info. retrieval
        - But, outbound connectivity from the data server is lax
- Inferential attacks
    - Recontruct the info. by sending particular requests and observing the resulting behavior of the Website / database server
        - Blind SQL injection
            - Infers the data present in a database system

## SQLi countermeasures

- Defensive coding
    - Manual defensive coding practices
    - Parameterized query insertion
    - SQL DOM (domain object model)
- Detection
    - Signature based
    - Anomaly based
    - COde analysis
- Run-time prevention
    - Check queries at runtime

# Database Access Control

# Inference

# Database Encryption

# Cloud Computing

# Cloud Security Risks and Countermeasures

# Cloud Security as a Service