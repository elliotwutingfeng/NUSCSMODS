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

<The address is computed at runtime>

- Limit register : tells if the address generated is outside of my range (Compiler can do)

Problems:
  - Memory has to be one big chunk (Contiguous)
  - Every memory access is an addition and comparison

<Limitation can be bypass if there are more registers>

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
