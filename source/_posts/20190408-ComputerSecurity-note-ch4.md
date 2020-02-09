---
title: '[Intro. to Computer Security Course Note] Ch 4'
tags:
  - NCTU
  - computer security
  - note
date: 2019-04-08 08:06:38
description: ' '
---

# Ch4. Access Control

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

- A general approach: access
    - Subjects vs. Objects
    - Each entry: access right
![](https://i.imgur.com/tq8TCV9.jpg)

## Decomposition Method 1

- Access controls lists (ACL): decomposed by columns (objects)
    - For each object, an ACL lists users and their permitted access rights
    - Default set of rights: users that are not explicitly listed
    - Convenient: determining which subjects have which access rights to a particular resource
    - Inconvenient: determining the access rights available to a specific user

![](https://i.imgur.com/qLg79Cx.jpg)

## Decomposition Method 2

- Capability tickets: decomposed by rows (subject)
    - A capability tickets specifies authorized objects and operations for a particular user
    - Convenient / inconvenient: opposite to ACLs
- Have greater security problem than ACLs. Why ?
    - Tickets may be dispersed around the system
        - Integrity of the ticket must be protected, guaranteed, and unforgeable
    - 2 solutions
        - OS holds all tickets on behalf of users
        - An unforgeable token in the capability

![](https://i.imgur.com/c8dOwQp.jpg)

## Another Approach: Authorized Table

就資料庫的感覺
![](https://i.imgur.com/dwSDlbg.jpg)

## A General Access Control Model for DAC

- 3 requirements
    - Representing the protection state
    - Enforcing access rights
    - Allowing subjects to alter the protection state in certain ways
- Concepts
    - As usual: a set of subjects, objects, and rules
    - New: protection state
- Protection states
    - Processes: delete, stop (block), and wake up
    - Devices: read / write, operation control, and block / unblock
    - Memory locations or regions: read / write
    - SubjectsL grant or delete access rights of objects

![](https://i.imgur.com/eqWUu9L.jpg)

## More Flexible Model: Protection Domains

- A set of objects together with access rights to those objects
    - r.g., Access matrix
- Recal security design principles: Least privilege
    - Every process and every user of the system should operate using the least set of privileges necessary to perform the task
- More general concpet: __minimize the access rights that any user of process has at any one time__
- Association between a process and a domain can be static or dynamic
    - e.g., Aprocess: a sequence of procedures require different access rights
- One form: distinction mode in many OSes (e.g., UNIX)
    - User mode: certain areas of memory are protected amd certain instructions may not be executed
    - Kernel mode

# Example: UNIX File Access Control

- UNIX files are administered using inodes (index node)
- Directories are structured in a hierarchical tree

## Traditional UNIX File Access Control

- UNIX user: a unique user identification number (user ID)
    - A member of a primary group, and possibly other groups
    - Each group is identified by a group ID
- Each file / directory: 12 protection bits
    - FIrst 9 bits: read, write, execute
    - Last 3 bits: setUID, setGID, and sticky bit
    - ![](https://i.imgur.com/BjGSBEo.jpg)
- SetUID / SetGID bits
    - Known as the effective user ID and effective group ID
    - System temporarily grants a real user with the rights of the file owner / group in addition to the real user's rights
    - For directories
        - SetGID: newly created files will inherit the group of this directory, rather than the primary group ID of the user who created this file
        - SetUID is ignored
- Sticky bit
    - Files: the system should retain the file contents in memory following execution (no longer used)
    - Directories: only the owner of any file in the directory can rename, move, or delete that file
- superuser
- Issues
    - No scalability, difficult to manage (user group 會弄得很冗)

## Modern UNIX Access Control: Access Control Lists (ACLs)

- Supported by many modern UNIX-based OSes
    - Extended ACL vs. minimal ACL (traditional)
- FreeBSD
    - Any number of users and groups can be assigned to a file
        - Each with 3 protection bits
    - A file need not have an ACL, may be protected solely by traditional access control
    - An additional protection bit: whether the file has an extended ACL
- Extended ACLs are used with the following strategies
    - Owner and other classes remain the same
    - Group class specifies the permissions for the owner group for this file
    - Additional named users and named groups may be associated with the file
    - ![](https://i.imgur.com/0guYtCw.jpg)

# Role-Based Access Control

- __Based on the roles that users assume__, instead of their identities
- Widespread commercial use and an area of active research
- __Many-to-many relationship__
    - Users to roles
    - Roles to resources

## RBAC Reference Models

- 4 modes
    - RBAC~0~: minimum functionality
    - RBAC~1~: RBAC~0~ + role hierarchies
    - RBAC~2~: RBAC~0~ + constrains
    - RBAC~3~: RBAC~0~ + RBAC~1~ + RBAC~2~
    - ![](https://i.imgur.com/iRzlddw.jpg)

## RBAC~0~: Base Model

- User: an individual that has access to this computer system
- Role: a named job function (authority level)
- Permission: an approval of a particular mode of access to one or more objects
- Session: a mapping between a user and set of roles to which a user is assigned

![](https://i.imgur.com/ILEUUqz.jpg)

## RBAC~1~: Role Hierarchies

- Roles with greater responsibility: greater authority to access resources

## RBAC~2~: Constrains

- Adapting RBAC to the specifics of administrative and security policies in an organization
    - Mutually exclusive roles
        - __A user can be assigned to only one role in the set__
        - __Any permission can be granted to only one role in the set__
        - __Non-Overlapping permissions__
    - Cardinality(基數)
    - Prerequesite role
        - e.g., __a user can be assigned to a higher role only if it is already assigned an lower role__

# Attribute-Based Access Control

- Define authorizations that express __conditions__ on properties of both the resource and the subject
- Strength: __flexibility, expressive power__
- Drawback: 運算較多，花時間

## ABAC Model: Attributes

- Subject attributes
    - A subject is an __active__ entity that causes info. to flow among objects or changes the system state
    - Attributes define the identity and characteristics of the subject
        - e.g., name, job title
- Object attributes
    - An object (or resource) is a __passive__ system-related entity containing or receiving info.
    - Objects have attributes that can be leveraged to make access control decisions
        - file name, file size, creator
- Environment attributes
    - The operational, technical, and even situational environment or context in which the info. access occurs
        - e.g., current date, time
    - Have so far been largely ignored in most access control policies

## ABAC Model: Distinguishable

- Controls access to objects by evaluating rules against the attributes of entities (subject and object), operations, and the environment
- Capable of enforcing DAC, RBAC, and MAC concepts
- Fine-grained access control: allows an unlimited number of attributes to be combined to satisfy any access control rule

## ABAC Logical Architecture

- 4 independent sources of info. used for the access control decision
- Powerful, flexible, __but cost is large__
- ![](https://i.imgur.com/oTcMBXC.jpg)

## ACL Trust Chain

![](https://i.imgur.com/Ae0QSIV.jpg)

## ABAC Trust Chain

![](https://i.imgur.com/z2rPj67.jpg)

## ABAC Policies

- A policy is a __set of rules__ and relationships that govern allowable behavior within an organization
    - Based on<br>1. Privileges of subjects<br>2. How resources or objects are to be protected<br>3. Under which environment conditions
- An ABAC policy model
    - ![](https://i.imgur.com/SRtbv2w.jpg)

# Case Study: RBAC System for a Bank