---
layout: post
published: true
title: 'CS2106 - Lecture 10: Virtual Memory management'
---
# Motiavation
Assumptions: 
1. The physical memory is large enoguh to contain one or more process with complete memory space

> Logical proccess >> physical


# Basic Idea

Secondary storage capacity >> Physical

- Split the logical address into smaller chunks
  - Some chunks reside in physical
  - Others are store in secondary
- This is like an extension of the paging scheme

### Extended page scheme
- Use page table: Virtual -> physical

New Addition:
- Two page types

- Memory resident (Pages in physical memory)
- Non memory resident (Pages in secondary storage)
- Use a (Is memory resident?) bit in page table entry

*We need to keep an extra bit to keep track of what the file can do*

- CPU can only access memory resident pages

Page - fault: When CPU tries to access non memory resident page

### Accessing Page X: General Steps
1. Check page table
   - Page x is a memory resident
   
   -> Yes: Access physical
   
   -> No : Continue
2. Page fault
3. Locate page in sec storage
4. Load page
5. Update page table
6. Reexecute the same instruction and go step 1


> ** In an multi-threaded system with many cores, when there is a trap to the OS, can some other thread run at the time. **

> The OS is not activitely fetching and running, there is a special piece of hardware call DMA controller which is programmed to bring certain memory without troubling the cpu, it will notify the CPU after it happens thus other process can continue to run even thou it is fetching memory. The process is not going to be involve any of the cpu cores.


The secondary storage access is very slow.

** If any 10 percent of pages are in main mem, what fraction of memory access will end up causing page fault **

If memory access result in page fault == Thrashing

#### Locality Principals
- Most of the time are spent on a small part of code
- In a time period, access are made to relatively small part of data

** Temporal ** 
Memory address which are use are likely to be use again

- Loaded to physical as it is likely to be access again

**Spatial**

Memory addresses close to a use address is likely to be used

- Page contains contiguous location that is likely to access in near future


# Page Fault

We can indicate which frame is needed from the secondary storage.

1. CPU request pages from MMU whcih contains the TLB and the logic to translate virtual to physical

2. MMU check if the page is in TLB, if its not it will fetch the page and replace it in its page table.

3. RAM is the physical memory

4. Disk is in the secondary storage


> The page table is stored in the part of the phyiscal memory where it is dedicated to the OS

We can have multiple parallel access and translation.
The OS is responsible for flushing the TLB when there is a context switch. 


#### Summary
- Complete seperate logical memory address from physical memory
   - Amount of physical memory no longer restrict the size of logical memory address
- More efficient use of phyical memory
   - Page currently not needed can be on secondary storage
- Allow more processes to reside in memory
   - Improve CPU utilization as more process are able to run

> The bottle neck could be memory as one process can use up all the memory, with virtual memory we can improve this and have more process running.


*If a thread experience a page fault does that means that all the other threads from the same process are block?*
> No

*What if we switch to another thread and it generates the same request that loads the same address*
> Trap to memory and OS will figure out that it does not need to do 2 request. They will sleep for all process that are waiting for that IO and there is an interrupt to wake up all waiting process once it is loaded. 


# Common application of Virtual Memory

## Demand Paging

The process is starting with all the pages in the secondary storage. When accessing it, will generate a page fault. Only when we need it, then we will bring the page into the physical memory. 

> Allows process to run unlimited virtual space on a machine with limited physical

There are alot of synchronisation involves when it comes to accessing memory and there are many codes in the linux kernel that ensure that the entire system is properly synchronised in OS level. OS cannot access a page that is being used, only when  the page is flush from a buffer then it can be access again. The buffer is called a victim cache.

**Which system designg principals demand paging follow**

> Laziness, this is very commonly use together with speculation in OS. This is only because we have not enough resources.
e.g Copy on write


- Huge page table with large logical memory space
   - Page table structures
- Limited number of resident memory space
   - Page replacement algo
- Limited physical memory frames
   - Frame allocation policies

# Aspects of virtual memory
## Page Table Structure
Page table infomation is kept with the process infomation and takes up physical memory space


If we have 2^p pages in logical memory space
- P bits to specify one unique page
- 2^p page table entries (PTE) with:
   - Physical frame number + additional infomation bits
   
### 2 Level paging
- Have a number of page tables that response to differenrt regions of the physical memory
- Reduce size of page tables
- Useful page must remain the space
- Reduce useless page

Split the virtual address into:
1. Base address

- Kept in register
- Use it to index the first structure

2. Pointer to page table
- Use to get the page frame number
- Index based on the base address
- Use the offset to get physical address

> there is no external frag and internal is inherited from pages

Cons:
- Need for 3 memory accesses
  - Page director
  - Page table
  - Physical

> The tree will grow and we have to traverse the tree until we find the page table. However, our TLB can bypass this. The one that is important is that the process must have a valid pointer.

*MMU caches are a complement to TLB which cache some part of the directory*


Pros:
- Less size used (from MB -> KB)

> Each page must be fit exactly correct, an invalid entry means that the entire subtree does not exist

We keep the infomation of how to translate from virtual to physical in the TLB


### Inverted Page Table

Given that we have a giant virtual address space compared to the physical. What if we have a structure that can tell us who occupies which virtual address givene the physical address and has a lesser overhead

- Page table is a per process infomation
- For every frame, remember who has access.

** Why do we need a process ID**

> We can have multiple process residing in the same page frame, this means they are sharing the same memory. We use the PID as an index in the inverted page table. We can use hash table to convert the physical address and guess from the inverted page table. 

- Verify the PID
- Verify the Page

**Are there any checks on the integrity of the page table?**

> The cache structure will have a valid bit that checks if the page entry is relevant or not.





## Page Replacement Algorithms
## Frame Allocation
