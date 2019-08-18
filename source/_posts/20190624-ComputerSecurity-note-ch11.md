---
title: '[Intro. to Computer Security Course Note] Ch 11'
tags:
  - NCTU
  - computer security
  - note
date: 2019-06-24 19:51:32
---

# Ch11. Software Security

---

# Software Security Issues

- Many vulnerabilities result from __poor programming practices__
- Consequences from insufficient checking/validation of data and error codes in programs

## Software Error Categories

- Insecure interaction between components
   - SQL injection
   - Cross-site scripting
   - Open redirect
- Risky resource management
   - Classical buffer overflow
   - Path traversal
   - DOwnload of code without integrity check
- Porous(多孔的) defenses
   - __Missing__ authentication for critical function
   - __Missing__ authorization
   - __Missing__ encryption of sensitive data

## Software Security: Software Quality/Reliability

- Software Quality and Reliability
   - Concern: accidental failure of a program
   - Not the total number of bugs, but __how often__ they are triggered
   - Improvement: structured design and testing to identity and eliminate bugs
- Software Security
   - Attacker targets specific bugs that result in a failure that can be exploited
   - Triggered by inputs that differ dramatically from what is usually expected
   - Unlikely to be identified by common testing approaches

## Defensive or Secure Programming

- The process of designing and implementing software: continue to function even when under attack
- Software written using this process
   - Detect erroneous conditions resulting from some attack
   - Either continue __executing safety, or fail gracefully__
- Key rule: __never assume anything__
   - Check all assumptions and handle any possible error states
- <table style="">
    <tr>
        <th style="font-weight: normal;">Typical programmers</th>
        <th style="font-weight: normal;">Defensive Programming</th>
    </tr>
    <tr>
        <th style="font-weight: lighter;">Attention on the steps needed for success<br>- Follow the normal flow of execution of the program<br>- But __not consider every potential point of failure__<br>Often make assumptions: type of inputs and environment</th>
        <th style="font-weight: lighter;">The assumptions need to be validated by the program<br>__All potential failures handled gracefully and safely__<br>But, increase codes and time spent</th>
    </tr>
    <tr>
        <th style="font-weight: lighter;">When changes are required<br>- Focus on the cahnges required and __what needs to be achieved__</th>
        <th style="font-weight: lighter;">Must carefully check any assumptions made<br>Check and handle all possible errors<br>Carefully check any interactions with existing code</th>
    </tr>
</table>
   
## Security by Design

- Recent years have been increasing efforts to improve secure software development process
   - Software Assurance Forum for Excellence in Code (SAFECode)
      - Outlining industry best practices for software assurance
      - Providing practical advice for secure software development

# Handling Program Input

- Incorrect handling is one of the most common failings
- Input is any source of data from outside and whose value is not explicitly known by the programmer
- All sources of input data must be identified
- Explicitly validate assumptions on size and type of values before use
- Two key areas of concern: __size and interpretation__

## Input Size & Buffer Overflow

- Programmers often make assumptions: __maximum expected size of input__
   - 有可能會導致 buffer overflows
- Testing may not identify the vulnerability
   - 測資不夠完整
- Safe programming practices
- __Safe coding regards any input as dangerous__

## Interpretation of Program Input

- Program input may be binary or textual
   - Binary data: __depends on encoding and is usually app-specific__
- Failure to validate may result in an exploitable vulnerability

## Injection Attacks

## Cross-site Scripting (XSS) Attacks

- __Input provided to a program by one user that is subsequently output to another user__
   - Assumption: all content from one site is __equally trusted__ and hence is permitted to interact with other content from that site
   - Attacks exploit this assumption and attempt to bypass the browser's security checks
- Most common variant: XSS reflection

## XSS Reflection

- Consider the widespread use of guestbook programs
   - 留言板那些的
- Prevention: any user-supplied input should be examined

## Validating Input Syntax

- Input data should be compared against __what is wanted__
   - using regular expression
   - Whitelisting __(more secure)__
- Alternative is to compare the input data with __known dangerous values__
   - Blacklisting

## Alternative Encodings

- Canonicalization: transforming input data into a single, standard, minimal representation
   - Once this is done the input data can be compared with a single representation of acceptable input values

## Validating Numeric Input

- Internally stored in fixed sized value
- Must correctly interpret text form
   - Have issues comparing signed to unsigned

## Input Fuzzing

- Major issue of input texting: very large range of inputs
- Fuzzing: a software testing technique: using randomly generated data as inputs to a program
   - Simplicity and freedom from assumption
   - Very low cost of generating large numbers of tests
- Input can be randomly generated
- Conceptually very simple, but identifying only simple types of faults
   - Only triggered by a small number of very specific input values

# Writing Safe Program Code

- Key issues
   - __Correct__ algorithm implementation, machine instructions
   - __Valid__ manipulate of data

## Correct Algorithm Implementation
- Not correctly implement all cases or variants of the problem
   - 用對的方法重做一遍

## Correct Machine Instructions for algorithm
- __Largely ignored by most programmers__
   - Assumption: 反正 compiler 會處理好
- Malicious compiler programmer
   - Including instructions in the compiler to emit additional code
- Countermeasure:
   - 檢查檢查再檢查(source 跟 machine code)

## Correct Data Interpretation

- All data on a computer are stored as groups of binary bits
- Different languages provide varying capabilities for restriction and validating interpretation of data in variables
- Correct use of memory
   - Issue: allocation and management of dynamic memory storage (heap)

## Preventing Race Conditions with Shared Memory

- Race condition

# Interacting with the OS and Other Programs

 In general, programs do not run in isolation on most computer systems

## Several issues

- Environment variables
   - 沒辦法透過 reset PATH variable 解決
      - `PATH="/sib:/bin:/usr/sbin:/usr/bin"`
      - 把 IFS environment variable 改調就可以繞過
   - Generally, writing secure, privileged shell scripts is very difficult
   - Dynamic linking of libraries may be vulnerable
      - Library injection (LD_LIBRARY_PATH)
      - Solution: using a __statically linked executable__ or __blocking the use of this env variable__ when the program executed runs with different privileges
- Using appropriate, least privileges
   - Root/Administrator privileges
      - __Major attack target__
      - Good design partitions complex programs in smaller modules with needed privileges
         - A greater degree of isolation between components
         - __Fewer consequences of a security breach in one component__
         - Easier to test and verify
- Systems calls and standard library functions
   - The programs may not perform as expected
      - Incorrect assumptions made for the operations of the system calls and standard library functions
- Preventing race conditions with shared system resources
   - Need suitable synchronization mechanisms
      - e.g., lock
   - Lockfile
- Safe temporary file use
   - Secure temporary file creation and use requires the use of __random names and atomic operation__
      - :+1: mkstemp()
      - :-1: ~~tmpfile(), tmpnam(), tempnam()~~
- Interacting with other programs

# Handling Program Output

- Programs must identify what is permissible output content
- Character set should be specified