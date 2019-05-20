---
title: '[Intro. to Computer Security Course Note] Ch 4'
tags:
  - NCTU
  - computer security
  - note
date: 2019-04-08 08:06:38
---

# Access Control

__Access control: the central element of computer security__

---

# Principal Objectives of Computer Security

- __Prevent unauthorized users__ from gaining access to recources
- __Prevent legitimate users__ from accessing resources in an __unauthorized manner__
- __Enable legitimate users__ to access resources in an __authorized manner__

# Access Control Principles

## Access Control Context

- __Authentication__: verification that user / system credentials are valid
- __Authorization__: the granting of a right or permission to a system entity ro access a system resource
- __Audit__: an independent examination of system records and activities
    - To test for adequacy of system controls
    - To ensure compliance with established policy and operational procedures
    - To detect breaches in security
    - To recommend any indicated changes in control, policy ans procedures

## Access Control Policies

- Discretionary access control (DAC)
    - __Based on the identity of the requestor__, and on access rules stating what requestors are (or are not) allowed to do
    - Why discretionary ? __An entity might have access rights to enable another entity to access some resource__
- Mandatory access control (MAC)
    - Based on security clearances of system entities, and on security labels of resources
    - Why mandatory ? An entity that has clearance to access a resource __may not enable another entity to access that resource__
- Role-based access control (RBAC)
    - __Based on the roles that users have__, and on rules stating what accesses are allowed to given roles
- Attribute-based access control (ABAC)
    - Based on attributes of the user, the resource to be accessed, and current environmental conditions

# Subjects, Objects, and Access Rights

## Subject

- An entity capable of accessing objects
- 3 classes
    - Owner
    - Group
    - World (include all users)

## Object

- A resource to which access is controlled

## Access Rights

- Describes the way in which a subject may access an object
- Could include
    - Read
    - Write
    - Execute
    - Delete
    - Create
    - Search

# Discretionary(任意) Access Control

- A general approach: access matrix

# Example: UNIX File Access Control

# Role-Based Access Control

# Attribute-Based Access Control

# Case Study: RBAC System for a Bank



