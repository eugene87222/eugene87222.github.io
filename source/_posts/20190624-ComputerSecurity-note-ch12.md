---
title: '[Intro. to Computer Security Course Note] Ch 12'
tags:
  - NCTU
  - computer security
  - note
date: 2019-06-24 19:57:00
description: ' '
---

# Ch12. Operating System Security

---

# Introduction

## System Security Planning

- The first step in deploying a new system is planning
   - A wide security assessment of the organization
   - To maximize security while minimizing costs
   - To determine security requirements for the system, apps, data, and users
   - To identify appropriate personnel and training to install and manage the system

# Operating System Hardening

- First thing to do: secure the base OS
- Basic steps
   - Install and patch the OS
   - Harden and configure the OS to adequately address the identified security needs of the system by
      - Removing 不必要的東西
      - Configuring 權限
      - Configuring 資源

# Application Security

# Security Maintenance

- NIST SP 800-123 suggests to include
   - Monitoring and analyzing logging information
      - Can only inform you about bad things that __have already happened__
   - Performing regular backups
   - Recovering from security compromises
   - Regularly testing system security

# Linux/Unix Security

- Patch management
   - Keeping security patches up to date is a widely recognized
- App security using a chroot jail
   - Some network accessible services: do not require access to the full file system, but rather only need a limited set of data files and directories
      - e.g., FTP
   - Running such services in a chroot jail: restricting the server's view of the file system to just a specified portion
   - Drawback: added __complexity__

# Windows Security

- Patch management
   - 記得更新

# Virtualization Security

- Benefits
   - 比較有效率
- However, it raises additional security concerns

## Hypervisor

- The software that sits between the hardware and the VMs
   - Acting as a resource broker

## Two Types of Hypervisor

- <img src="https://i.imgur.com/a5cfdKu.png" width="60%"/>
- Key differences
   - Typically, type 1 performs better, __more secure__, __用在 server 上__
   - Type 2: enabling virtualization without needing to dedicate a server to that function, __用在 client 上__

## New Type: Container/APp Virtualization

- <img src="https://i.imgur.com/tCGCtqx.png" width="60%"/>
- Reducing overhead: no need of resources to run a separate OS for each app
- But, 安全風險較高

## Securing Virtualization Systems

- Hypervisor security
   - Secured using a process similar to securing an OS
   - Installed in an __isolated__ environment