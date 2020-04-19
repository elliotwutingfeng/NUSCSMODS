---
layout: post
published: false
title: 'CS2106 - Lecture 11: File System'
---

# File System
## Motivation

Physical memory is volatile
- Use external storage to store *persistent* info

Direct access to the storage media is not portable
- Dependent on hardware specification and organisation

__We need to use another method to write and read, we need some layer to make it consistent for the user.__

> We need the OS to help us access these devices

File System provides:
- An abstraction
- A high level resource management scheme
- Protection between proccess and users
- Sharing between processes and users

### General Criterial
- Self contained
Should be able to plug and play
- Persistant
Beyond the life of OS and processes
- Efficient
Minimum overhead and good management of free/used space

## Vs Memory management

> The file system has to able to adapt.

> The memory is used by the process implicitly. (We do not know how to do it specifically, the OS will figure ut

![2106_11_1.PNG]({{site.baseurl}}/img/2106_11_1.PNG)



# File System Abstraction

We interact with the system all the time, we are able to see a abstraction of memory using file abstraction

- Repreent a logical unit of infomation created by process

> The user can create/edit/delete/read a file

An abstraction is an abstract data type (file) that has a set of common operation

Contains:
Data : Infomation
Metadata: Infomation regarding the data

## Metadata
![2106_11_2.PNG]({{site.baseurl}}/img/2106_11_2.PNG)


## Operations

# Directory
## Directory Structure