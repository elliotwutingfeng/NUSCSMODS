---
layout: post
published: true
title: 'CS2106: Lecture 7 - Memory Abstraction'
---
# Basic of Memory
## Hardware
- Physical memory storage: 
    - Random access memory (RAM)
    - Can be treated like an array of AU
    -  AU = addressable unity =  1 byte
    - Each byte has an unique index known as a physical address

<Insert slide 4>

### Actual Execution
The compiler does not know where the address is when a code is runned requesting access to an memory. Sometimes the compiler needs to store data as well, how does the compiler know which memory is free.
The OS will allocate the memory that is requested.

## Transient Data
Stack

## Persistent data
heap/global

## Managing memory
The OS

- Allocate to new process
- Manage space for process
- Protect memory space of process from each other
- Provides memory related syscalls
- Manage for internal use

# Memory abstraction

Memory abstraction is useful as it ensure protection for a memory space. 
Some embedded system however, does not use memory abstraction. This allow full control of the memory and allow the system to directly access (No OS in between)
However, this is bad as might as two process might fight for the same physical address if run together.

*We can fix this issue by adjusting the address base on what is given (Offset)*

- Recalculate the memory reference during loading
Problems:
  - It might be slow to load
  - Not easy to distinguish memory reference from normal integer constant

- Base + Limit register

Write my code such that every code is relative from the starting point of my code
- Base register: Stores starting address of my program


>The address is computed at runtime

- Limit register : tells if the address generated is outside of my range (Compiler can do)

Problems:
  - Memory has to be one big chunk (Contiguous)
  - Every memory access is an addition and comparison

>Limitation can be bypass if there are more registers

However, this idea is very useful
  - Segmentation mechanism
  - Provides a crude memory abstraction
* Address 4096 in process A and B are no longer the same physical location *
  

## Logical Address
- Embedding actual physical address in program is a bad idea
   - Give idea to the logic of logical address

We want to involve the operating system but we do not want to pay the price of it


# Contiguous memory abstraction
  
## Assumptions
- Process must be in memory during execution
   -  Store memory concept
   - Load-store Memory execution model

1. Each process occupies a contiguous memory region
2. The physical memory is large enough to contain one or more processes


## Memory partitioning
Contiguous memory region allocated to a single process

### Fixed size partition
   - Physical memory is split into fixed number of partitions
   - Process will occupy one of the partitions

*Chunk the memory into partitions of equal size, we can fit a process into any of the partitions with no differentiation*
*A process however, may not be able to fit in due to the fix size or it might waste some space*
*This is a waste problem called internal fragmentation*

Advantage:
- Easy managed
- Fast to allocate
    - Due to fixed size, there is no need to choose (No algo run)

Disadvantage
- Internal fragmentation (Smaller process will waste memory space)
- Partition size need to be large to accommodate the process

### Dynamic Partitioning


   - Partition is created based on the actual size of process
   - OS keep track of the occupied and free memory regions
      - Perform splitting and merging when necessary

- Dividing the memory to different sizes
- Assign the needed memory for the processes
- This resolves the problem of internal fragmentation

>However, if a process frees a space, the memory that it frees + the leftover memory is enough to accommodate a process but due to the fragmentation, it is not useable (External Fragmentation)

Pros:
- No internal fragmentation
- Flexible

Cons:
- There might be secondary external fragmentation
- Need to maintain more info in the OS
- Takes more time to locate appropriate region

*It is much more challenging for OS to manage partitions of many sizes*


*We can have almost infinite number of partitions but it is very hard for the OS to manage. It has to store the partition into a linked list.*


#### Allocation algorithms

- Assuming the OS maintains a list of partitions and holes
- Algo to locate partition of size N
- Variants:
  - First Fit
   
    Pick the first hole that is large enough
   - Best fit

    FInd the smallest Hole that is large enough
   - Worst fit
    
    Find the largest hole
- Split the hole into N and M-N
    - N will be the new partition
    - M-N will be left over space -> a new hole

#### Merging and Compaction

> This are ways to solve external fragmentation after dynamically allocating

When an occupied partition is freed:
  - Merge with adjacent hole if possible

Compaction:
  - Move the occupied partition around to create consolidate holes
  - Cannot be invoked to frequently as it is time consuming
