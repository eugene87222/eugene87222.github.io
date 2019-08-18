---
title: '[Intro. to Computer Security Course Note] Ch 3'
tags:
  - NCTU
  - computer security
  - note
date: 2019-06-24 19:33:38
---

# Ch3. User Authentication

---

# Definition

- Thee process of verifying an identity claimed by or for a system entity
- Consist of two steps
    - Identification step: presenting an identifier to the security system
    - Verification step: presenting or generating authentication info. that corroborates(鞏固) the binding between the entity and their identifier

# Electronic User Authentication Model

![](https://i.imgur.com/kCuOAL5.jpg)

## Cornerstone

- Credential
    - Paper credential<br>e.g., 護照那些、身分證
    - E-authentication credential: an object or data structure
        - Authoritatively binds an identity (via an identifier) and (optionally) additional attributes
        - To at least one token (or authenticator) possessed and controlled by a subscriber
- Token
    - __Something that the Claimant possess and controls is used to authenticate the Claimant's identity__
    - Typically a cryptographic module or __password__
    - Also named as __authenticator__
- Authentication establishes confidence that the Claimant has possession of an authenticator(s) bound to the credential, and (optional) the attribute values of the subscriber
- ![](https://i.imgur.com/4JUgWvd.jpg)

## Role of each Entity

![](https://i.imgur.com/aS8wmR5.jpg)

## Tokens (Authenticators)

Something the individual know, possess, is, does

## Digital Identity Model

# Password-based Authentication

## The User ID

- __Determines the user's privileges__
- Used in discretionary access control

## Attacks / Countermeasures

- Offline dictionary attack
    - Obtain the system's password file (password stored in hash value)
    - Search for valid passwords with hash values of commonly used passwords
    - Countermeasure:<br>prevent unauthorized access to the password file<br>intrusion detection measures to identify a compromise
- Specific account attack
    - 一直 try 密碼 try 到對為止，或是被 ban
- Popular password attack
    - Try popular passwords against a wide range of user IDs
    - Countermeasure:<br>inhibiting the selection by users of common passwords<br>scanning the IP addr. of auth requests and client cookies for submission patterns
- Password guessing against single user
    - Gain knowledge about the account owner and password policies and use them th guess the password
    - Countermeasure:<br>enforcement of password policies that make passwords difficult to guess
- Workstation hijacking
    - Wait until a logged-in workstation is unattended
    - Countermeasure:<br>automatically logging the workstation out after a period of inactivity
- Exploiting user mistakes
    - 把密碼寫在桌上、把密碼傳來傳去(Email, SNS)、用預設密碼
- Exploiting multiple password uses
    - Different network devices share the same or similar password for a given user
    - Countermeasure:<br>__JUST DON'T__
- Password sniffing / phishing
    - Passwords are transmitted without ecryption (http, ftp)
    - Phishing web pages
    - Countermeasure:<br>encryption, inputting passwords with trusted devices and environments

## Use of Hashed Passwords

A widely used password security technique
![](https://i.imgur.com/pXvHbHR.jpg)

- Salt
    - Prevent duplicate passwords from being visible in the password file (同樣的密碼會有不同的 hash code)
    - Greatly increases the difficulty of offline dictionary attacks
    - Nearly impossible to find out wether a person has used the same password on multiple systems
- 2 threats
    - Password guessing on the machine
    - Password guessing on another machine

## Old Implementation of UNIX Password Scheme

- Password: up to 8 characters
    - Serving as the key input to DES
- Modified DES encryption
- Repeated for a total of 25 encryption (slow hash function)
- Has been regarded as inadequate (key length is too short)

## Improved Implementation

- Recommended hash function is based on MD5
    - Salt: up to 48-bit
    - Password length unlimited
    - __128-bit hash value__ -> __increase overhead for cracking__
    - Slowdown: an inner loop with 1000 iterations
- Bcrypt: developed for OpenBSD based on the Blowfish symmetric block cipher
    - Most secure version of UNIX hash / salt scheme
    - __128-bit salt, 192-bit hash value__ -> __increase overhead for cracking__
    - Configurable cost variable (number of iterations) -> depends on how important the password is

## Password Cracking of User-chosen Passwords

- Traditional appoaches
    - Dictionary attack
        - Countermeasure:<br>__slow hash function__
    - Password crackers exploit that fact that people choose easily guessable passwords
    - Rainbow table attacks
        - __Pre-compute__ tables with hash values for all salts
        - Countermeasure:<br>a sufficiently __large salt value and large hash length__
        - Combination of brute-force and dictionary

## Modern Approaches for Password Cracking

- Complex password policy

## Major Countermeasures

- Password file access control
    - 2 mechanisms
        - Access control: makes the password file availble only to privileged users
        - __Shadow password file (store the hash code separately)__
    - Vulnerabilities
        - Weakness in the OS that allows access to the file
        - Accident with permissions making it readable
        - Users with same password on other systems
        - Weakness in physical security may provide access to backup media
        - Sniffing network traffic
- Password selection strategies
    - User education
    - Computer-generated passwords
    - Reactive password checking
        - System preiodically run its own password cracker to find guessable passwords
    - Complex password policy or proactive password checker
- Proactive password checking
    - Rule enforcement
        - But, attacker can follow the guideline to design cracker
    - Password cracker
        - Compile a large dictionary of __bad__ passwords not to use
        - But, it is __space-consuming and time-consuming__
        - Can we use a hash function to address the issue ? 
            - Yes, can only reduce time
    - Bloom filter: a space-efficient probabilistic data structure
        - Used to test whether an element is a member of a set
        - A bit array of _m_ bits, and _k_ different hash functions
        - But, __false positive matches are possible__
        - Space adventage: do not store the data items
    - Applied to the password checking
        - Used to build a table based on dictionary
        - Check desired password against this table

# Token-based Authentication

<table style="">
    <tr>
        <th style="font-weight: normal;">Card Type</th>
        <th style="font-weight: normal;">Defining Feature</th>
        <th style="font-weight: normal;">Example</th>
    </tr>
    <tr>
        <th style="font-weight: lighter;">Embossed</th>
        <th style="font-weight: lighter;">Raised characters only, on front</th>
        <th style="font-weight: lighter;">Old credit card</th>
    </tr>
    <tr>
        <th style="font-weight: lighter;">Magnetic stripe</th>
        <th style="font-weight: lighter;">Magnetic bar on back, characters on front</th>
        <th style="font-weight: lighter;">Band card</th>
    </tr>
    <tr>
        <th style="font-weight: lighter;">Electronic memory</th>
        <th style="font-weight: lighter;">Electronic memory inside</th>
        <th style="font-weight: lighter;">ATM, credit cards</th>
    </tr>
    <tr>
        <th style="font-weight: lighter;">Smart Contact / Contactless</th>
        <th style="font-weight: lighter;">Electroni memory and processor inside<br>Electronic contacts exposed on surface<br>Radio antenna embedded inside</th>
        <th style="font-weight: lighter;">SIM card, Biometric ID card</th>
    </tr>
</table>

## Memory Cards

- Functions
    - Can store __but do not process data__ (都說是 memory 了)
    - Can include an internal electronic memory
- Most common: the bank card with a magnetic stripe on the back
- Usage
    - Alone for physical access (e.g., hotel room)
    - Combined with a password or PIN: provides significantly greater security
- Drawbacks
    - __A special reader is required__
    - Token loss
    - User dissatisfaction

## Smart Tokens

- Categorized along four dimensions
    - Physical characteristics
        - Include an embedded microprocessor
    - User interface
    - Electronic interface
        - __Required by a smart card or other to communicate with a compatible reader / writer__
        - Contact: direct contact between a card reader and a conductive contact plate on the card
        - Contactless: both the reader and the card have an antenna
    - Authentication protocol
        - Static
            - User authenticates himself or herself to the token
            - Token authenticates the user to the computer
        - Dynamic password generator
            - __Token generates a unique password periodically (e.g., every minute)__
            - Initialized and synchronized for the token and the computer
        - Challenge-response
            - __Computer generates a challenge__
            - __Token generates a response to the challenge__

## Most Important: Smart Cards

- Contains an __entire microprocessor__
    - Including processor, memorym I/O ports
- 3 types of memory
    - Read-only memory (ROM)
    - Electronic erasable programmable ROM (EEPROM)
    - Random access memory (RAM)

![](https://i.imgur.com/WKdF0eh.jpg)

# Biometric Authentication

- Based on unique physical characteristics
    - Static: fingerprints, facial characteristics
    - Dynamic: 聲音有的沒的
- Relies on pattern recongnition technologies

![](https://i.imgur.com/gjbBlcI.jpg)

# Remote user Authentication

More security threats
General solution: challenge-response protocols
![](https://i.imgur.com/jmhl7HR.jpg)
![](https://i.imgur.com/X0fPVz2.jpg)

# Security Issues for User Authentication

- Client attacks: masquerade as a legitimate user
    - Countermeasure: strong passwords and limited attempts
- Host attacks: steals the user file where passwords, token passcodes, or biometric templates are stored
    - Countermeasure: strong access control
- Eavesdropping(竊聽)
    - Countermeasure: multifactor authentication and anomaly detection
- Relay: repeats a previously captured user response
    - Countermeasure: a random number in challenge-response protocols
- Trojan horse: installation of rogue cilent or capture device
    - Countermeasure: authentication of client or capture device within trusted security perimeter
- Denial of service: lockout by multiple failed authentications
    - Countermeasure: multifactor with token