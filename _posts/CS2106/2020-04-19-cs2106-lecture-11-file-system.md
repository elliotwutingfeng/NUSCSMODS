---
layout: post
published: true
title: 'CS2106 - Lecture 11: File System (User)'
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

Difference in file management vs using inline CLI

- File management is not case sensitve
- File management cannot use non alphabetical characters (e.g *)


There are special files:
- NULL: remove all files inside
- Random: Gives you random numbers that are gathered from your hardware noise

> The windows file system look at the extension to figure out what file it is but the Linux file system looks at the meta data to figure out what file it was

### Permission bits
- Reading/Writing/Execution

1. Owner: The user who created the file
2. Group: The set of users who need similiar access to file
3. Universe: All other users in the system


`chmod 777 *`

This would give permission the everyone

Using the `ls -l` command would allow you to see all permission

### Access control List
In Unix, ACL can be
- Minimal ACL (The same as permission bits)
- Extended ACL added named users/group)

![2106_11_3.PNG]({{site.baseurl}}/img/2106_11_3.PNG)

## Structure
- Array of bytes

Each byte has a unique set of data

- Fixed length records

 Array or records, each record has an offest whcih can be calculated from the size of record * (N-1).
 
 Records will grow and shrink
 
 - Variable length records
 
 Records are of different size.
 This is flexible but it is harder to locate a record.
 
 
 > Fix = internal, variable = external fragmentation
 
## Access Methods
 
#### Sequential access
 - Data is read in order, staring from the beginning
 - Cannot skip but can be rewound
 
 > This is like a tape, in order to get to a location n, you have to start from the beginning 
 
#### Random Access
 - Data can be read in any order
 - Read (offset): Every read operation explicitly state the position to be access
 - Seek(offset): A special operation is provided to move to a new location in file
 
 e.g Unix and Window uses seek
 
 
#### Direct Access
 - Use for file contains fixed length record
 - Allow random access to any record direclty
 
 This is useful where there is a huge amount of records
 
- The basic random access method can be view ass
each record == one byte

### Generic Operation

![2106_11_4.PNG]({{site.baseurl}}/img/2106_11_4.PNG)

### System calls

We can use file operation via system call.
e.g

`open(filename, O_RDONLY)`
`write(STOUT_FILENO, strBuff, strleng(StrBuff))`
`read(fd, &charBuf, 1)`
`close(fd)`

Os provides file operation as system calls 

- Protection, concurrent and efficient access
- Maintain infomation

Infomation kept for an open file:
- File pointer (Current location in file)
- Disk location
- Open count (How many processes has open the file)

Consider:
- Several process can open same file
- Several different files can be open


Common approach
- System wide open file: One entry per unique file
- Per proccess open-file table: Know what process is doing to that file, this is per file.

> there must be a link for these two tables


      But why must we have same fd for the child and parent before fork???


# Directory
- Provide a logical grouping
- Keep track of files


## Directory Structure

### Single level
![2106_11_5.PNG]({{site.baseurl}}/img/2106_11_5.PNG)


### Tree structure
![2106_11_6.PNG]({{site.baseurl}}/img/2106_11_6.PNG)

(Linux)

Absolute path: Starts with a /

Relative path: Does not start with /

> this is a tree because each node has a parent

### DAG
![2106_11_7.PNG]({{site.baseurl}}/img/2106_11_7.PNG)

> This allow us to create a link such that we can access the file when it is deeper in the tree

- But this will cause the file to have multiple parents

File can be shared

#### Hardlinks

The file will parented by two folders.

Pros:
- Low overhead, only pointers are added in directory

Cons:
- Deletion problems: We need to delete both links if not one link will become null (invalid)


#### Symbolic link

- Add a `-s` to the unix command
- Creation of this link will need an additional file that contains the path to the linked file.


Pros:
- Simple deletion


Cons:
- Large overhead: We need to create a new file

> This is allowed to be created for folders

![2106_11_8.PNG]({{site.baseurl}}/img/2106_11_8.PNG)

- There is cycle
- We need to stop when there is a cycle 

> now of the days, LS is programmed to stop it when there is a cycle

### General Graph

- Not desirable
- Hard to traverse
- Hard to determine when to remove a file/directory

In Unix:
- Symbolic link is allowed to link to directory



