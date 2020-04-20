---
layout: post
published: true
title: 'CS2106 - Lecture 12: File System Implementation'
---
- File systems are stored on storage media
- Concentrate on hard disk


## Layout

- General Disk Structure

  - 1-D array of logical block
  - Logical block : Smallest accessible unit (512 bytes to 4KB)
  - Logical block is mapped into disk sector
     - Layout of disk sector is hardware dependent


![2106_11_9.PNG]({{site.baseurl}}/img/2106_11_9.PNG)



## Disk Oraganisation
> There is an array of logical block which is divided into partition.
Each partition has a MBR (Master Boot Recognisation)

MBR contains:
- Partion table
- Simple boot code

Partion contains:
- OS Boot block: Every partiton can have a different file system
- Partition details: Tells whats the free space/how many blocks in total/what type of file system
- Directory structure: How exactly the infomation is stored for a particular file type
- File Info: What block each file is using/name/permission
- File Data

> note that the infomation can be mixed together




# Implemntation details

A logical view of a file is a collection of logical blocks. 

When the file size is not a multiple of logical blocks, the last block might have *internal fragmentation*

> What ever we have at the last block is a wasted space that cannot be use. (Due to the overhead)


A good file implementation must:
- Keep track of logical blocks
- Allow efficient access
- Disk space is utilized effectively (Little overhead)

## File infomation

### Contiguous Block Allocation

Allocation must be contiguous. It will be very easy to access (Just by going to the offset)

Just give consequtive blocks.

Infomation to store:
- Start: Where is the starting point?
- Length: How long is the data?

> What is the maximum file size for file "tr" in the current slide
Answer: 5, because its the number of space free behind it


We can see that the file size is fixed when allocated.

Pros:
- Manage easy
- Access Easy
- Easy traverse

Cons:
- Fixed size (Cannot grow much) specified in advance
- Might have issues due to external fragmentation

### Linked List Allocation

Infomation:
- Start
- End (For appending)
- Use a pointer

Pros:
- Can grow

Cons:
- Traversal problem (slow)
- Overhead (Pointer)
- If one block is corrupted, the rest is lost


### File block Allocation: Linked List v2.0

![2106_11_10.PNG]({{site.baseurl}}/img/2106_11_10.PNG)

- Having a link list as a seperate structure 
- Known as FAT (File allocation table)
- Block pointers is stored in a single table
- The last file is signified by the -1

Pros:
- Can be kept in memory (Finding the next block is faster)
- Simple and efficient
- Light weight

> the array like structure is stored in memory thus we do not need to keep accessing the disk 


Cons:
- If each entry is 4 bytes, we will have 3GB needed for the fat table

### Index Allocation
- Have an block called index block which show where the infomation is stored
- Use of index table
- IndexBlock[N] == Nth block address

Pros:
- Less memory overhead
- Fast direct access

Cons:
- Limited Maximum file size
   - Max no. of blocks == no. of index block entries
- Index block overhead

Other schemes:
- Multilevel index: Similiar to multi-level paging
> One disadvantage is that we need n number of access if there are N levels
- Linked scheme
- Combined scheme: Combination of direct index and multilevel

![Combined Scheme]({{site.baseurl}}/img/2106_11_11.PNG)



## Free Space management
- Know which disk block is free

Allocate:
- Remove free disk block from free space list
- Needed when file is created or enlarged (appended)

Free:
- Add free disk block to free space list
- Needed when file is deleted or truncated

### BitMap
- Each diskblock is represented by 1 bit 

        0 - occupied
        1 - free

Pros:
- Good set of manupilition

Cons:
- Keep in memory

### Linked list
- Use a link list of disk blocks
- Each disk blocks contains:
   - A number of free disk blocks number
   - Pointer to the next free
   
![2106_11_12.PNG]({{site.baseurl}}/img/2106_11_12.PNG)

Pros:
- Easy to locate free block
- Only first pointer needed in memory
- Other blocks can be cache for efficiency

Cons:
- High overhead


# Directory Structure
- How we store the directory structure
> Directory is part of the file system but it is not only one part that stores purely directory
This help us to tell us how the files are stored

- Keep track of files in directory
- Rememeber this in some structure way


# File System in Action

# Disk I/O Scheduling
