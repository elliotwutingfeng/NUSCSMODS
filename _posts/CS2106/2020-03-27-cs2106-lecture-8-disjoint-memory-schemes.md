---
layout: post
published: true
title: 'CS2106 - Lecture 8: Disjoint memory schemes'
---
Now we are under the assumption that everything is fixed sized partition
1. The physical memory is large enough to contain one or more processes

#Paging scheme
##Introduction
The physical memory is split into region of  **fixed size ** 
- Known as physical frames
- Frames size decided by hardware

> Memory designers or hardware designers decide the size? -> CPU decides the frame size as it is the component that does the translation.
The logical memory of a priccess is split to
- Same size
- Logical page

At the exe time, the pages of process are loaded into any available memory frame
- Logical is contiguous
- Occupied physical memory region is disjoint

### Page Table: Look Up mechanism

Contiguous:
- Simple to keep track of the usage of process
    - Starting address and size of process
    - Using simple link list storing mem context information for all process

Paging scheme:
- Logical page <-> Physical frame mapping is no longer straightforward
- Need lookup table to translate
- This is page table

*Physical memory is divided into frames where each page in the logical memory is mapped into a frame.* 

> What is the physical address in memory that will be access when the process is loaded. -> 
Given page size is N = 1000B,
 if the address is loaded is 

                          load r1, [2106] 

It will be in page 2 since it is in 2000's memory where
page 0 -> 0 to 1000
page 1 -> 1000 to 2000
page 2 -> 2000 to 3000


> As you can see there is no reference about the physical memory nor the amount of byte we are accessing since each page is the same size. 
## Logical Address Translation
It is easy to compute the physical address given the size of the page and the logical address.

Physical address = **frame_number X sizeof(PhysicalFrame) + offset**

Logical memory address :
- Page (m)
- Offset (o)

e.g 
given logical address of 1110 where m = 4, o = 2

11 -> frame number
10 -> Offset

Look at the frame number 11 (3) and see what address it is map to.

*assume page 3 maps to 110*

Physical memory of this address will be -> 110 + offset = 110 + 10


### Tricks
- Keep frame size (page size) as power of 2 
- Physical frame size == logical page size

> If a size of a page is 2^n then we need n bits to identify


### Observation
- There are no external fragmentation -> There is no contiguous memory
- There are internal fragmentation -> We can have a process memory that use not the entire page (internal fragmentation)

> It is common but it is not a big issue as page is normally allocated to be larger than whar a process need. It is better than fix partitioning as for page, internal fragmentaion only happen to the last page

- Clean seperation of logical and physical address space
  - great flexibility
  - Simple address translation

### Implementation
- OS stores page table in PCB
- Memory contact of a process == page table

> We do not store the entire of the memory nor copy it into the PCB. 

Issues:
- Requires 2 memory access for every memory reference
   - Page
   - Physical

> inc src uses 6 memory access 
  - Instructions
  - Get value from register
  - Translation


(disjoin p1_

## Hardware Support
- TLB (Translation  look aside buffer)

Instead of going to memory and do translation multiple times, we just check the cache.
TLB cache page table entries and is very small and fast (<=1 clock cycle)

> It is one if the fastest structures in the computer

- Logical address translation with TLB
   - Use page number to search TLB associatevely
   - Entry found (TLB-HIT)

Frame number is retrieved

   - Entry not found (TLB-Miss)
 
Memory access to access the full page table. Retrieve frame number is use to generate physical address and page table


#### Translation

**Without**

1. CPU generate page number and offset
2. Use the P to index the table and the frame number
3. Go to the physical memory and get the memory using the frame and offset


** With (Hit)**

1. CPU generate page number and offset
2. Pypass the memory and go straight to the cache
3. Access using the offset



AMAT (Average mem access time) 

**= P(TLB hit) X latency (TLB hit) +  P(TLB miss) X latency (TLB miss)**

> There is a hidden time which is not considered which is the time taken to fill the TLB

#### During Context Switch:
Phy:
- No difference
- No saving


Log:
- No change
- They are pointing


PT
- Reside in OS memory
- The OS will not save and restore it all the time
- OS will use a reg in the CPU that record the PT starting index
*Sort of like loading a stack*

TLB:
- Hardware optimisation that help with optimisation
- They are invisible to the software/application
- The TLB might be misguided to some memory that does not belong to that process and cause seg fault after context switch thus we need to do TLB flushing that will be done by the OS.


> TLB is not part of the hardware context of a process although the OS must know about it.

> It is one TLB per CPU core

## Protection and Page Sharing
- Access right bits

Is the page exist and whether the page is readable, writable or executable bits. Memory access is checked against these access right bits.

- Valid bit

> Logical memory range is usually the same for processes.

Only pages that can be use have the bit set, if we try to translate any page that has 0 bit set, then it will thrown an exception


### Page sharing

- Page table can allow several process to share the same physical memory frame:

Some code is shared within multiple processes (syscall) 

**Copy on write**

- Create the a new page of a child process only when the child wants to write. Accessing (reading) will use the same page table as the parent

# Segmentation Scheme
Instead of fitting the process in variable size partition, we break the process to fit into multiple variable size partition
## Motivation
Each process has a distinct number of logical memory regions (stack, data, text, heap)
We just need to have a distinct section to access

- text : Read
- Data: RW
- Heap/Stack: R/W

However, some regions may grow and shrink at execution time and this is not good for paging due to potential internal fragmentation.
Usage and permission within a segment are usually the same.
## Basic Idea
Manage memory at the level of memory segments
- Logical memory space of proccess is a collection of segments
- Mapped into contiguous physical partitions of the same size

Each memory segment:
- Has a name
- Has a limit (How far it can grow)

All (Logical) memory reference is specified as:
- Segment name + offset

- Neither the compiler nor the compiler needs to know where the segments are located, only that it exist. The compiler does not need to know about the logical address associated with the address.
The os will place the segment into an available space in pjysical address and this is when it is known (Base address)


## Logical Address translation
Each segment mapped to a contiguous physical memory region
- Base address
- Limit

The segment name is represent as a single number
- seg id

Logical address <segID, Offset>
- segID is use to look up base and limit of the segment in a segment table
- Physical address is base + Offset
- Offset < limit for valid access ( Cause of seg fault if it is above limit)

> Looking up the segment table using the segID where we will check the limit.

e.g <2,500>
Segment 2 has the base address of 2400

Our lookup -> 2400 + 500 in physical address

## Hardware support
We need to lookup memory twice for each lookup
1. Segment table
2. Access after doing translation

> This is much more efficient

## Differences

###Pros:
- Each segment is independent continguous memory space

More efficient bookkeep and segments can be protected/shared independently
This also matches a programmer's view of memory

> Depends on the size of the memory, it determines the number of factor if to go for segmenting or paging



### Cons:

- Can cause external frag due to variable size contiguous memory

# Segmentation with Paging scheme
Problems with segmentation: We are still trying to fit a segment into a fix size partition.
Instead we break every segment into pages 

## Basic Idea
- Every segment have its own page table
- Mapping each pages into physical memory

Pros:
- Easy to shrink and grow segments

1. Process generate the logical address -> <Segment, pagenumber, offset>
2. Get the memory in segment table
3. Get the page number from the segment
4. Add the offset to get the physical memory

> There are alot of strcuture for the OS to work with
<disjoint>
