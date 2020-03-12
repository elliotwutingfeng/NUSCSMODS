---
layout: post
title: CS2106 Lecture 1 - Introduction to OS
subtitle:
---

# What is OS

A program that acts an intermediary between a computer user and the computer hardware.

A system stack has a lot of layers and each of them can act as intermediary. It manages computer hardware, software resources and provides common services. It is a system software.

*OS is an abstraction provided for the users.*

OS allow the user program to interact with the hardware.
*The first few computer invented does not have an OS to interact with the hardware. There is an advantage of minimal overhead but it is not portable and is inflexible. It is also efficient in its use of computer resources.*


# OS for Mainframes

<Insert 10>

Batch OS to execute the user program one job at a time

Common features:
- No interactive interface
- Accepts programs in forms of tapes
Improvements
- CPU Idle when Performing I/O (Inefficient for simple batch processing)
- Multiprogramming 
Multiple programs 
- Time-sharing (1970s)

# Multiple users

## Time-sharing OS

Features:
- Allow multiple users
- Job schedule
- Memory management

*The operating system have to give an illusion that you are alone and that no one else is using the same system. But the machine is running in parallel with someone. This is called parallel hardware.*
- Multics

Parent of UNIX

*It is the job of the OS to provide resources like memory to the users. Virtualization means that the program can see the hardware as if it is running by itself. It is not impacted by other programs other than the speed.*

## Minicomputer and UNIX
- Evolution of moors' law
- The smaller and cheaper mainframe


## Personal Computer

Machine dedicated to user and not timeshared between multiple users, 
give rise to personal OS

- Windows model
- UNIX model

# Motivation for Operating System

"Things don't work without OS"
Abstraction
- Large variation in hardware configuration

The OS Abstract away the complex features
OS give a uniform abstraction

## Provides
- Efficiency

*Managing the system, the abstraction of allowing multiple users use the system makes it useful*

- Portability

- Resource allocator

The program execution requires many resources
Multiple programs allowed to execute simultaneously
- Manage all resources
- Arbitrate potentially conflicting request

To be fair and efficient between users 
Control Program
Program can misuse the computer.

## Security and protection
- Accidentally: Coding bugs
- Maliciously: Virus, malware

OS is a control program, it controls the execution of programs
- Prevent errors and improper use of computer
- Provides security and protection

# OS Structure

## System Structure
- Flexibility

*How general and flexible*
- Robustness

How extensive
- Maintainability

*How much do we need to upgrade, is it easy to update, is it easy to add a new component*

- Performance, scalability

*Dimensions, the number of memory of number of threads supported.*

![Slide 27](/NUSCSMODS/img/CS2106/1-27.png)

*The kernal is the core of the OS that exposes some of the interface to the underlying hardware and the interfaces. There are some important system softwares that are not part of the kernel.*
*Running in kernal mode means to have all the privileges.*


![Slide 28](/NUSCSMODS/img/CS2106/1-28.png)

*The User programs itself have its own API so the user can call, the library in return talk to other library. The library is a software and is a piece of precompiled code. Some lib needs to do a system call and talk to the os and in turn talk to the hardware. These calls are called syscalls.*

*The reason why we have these calls is because sometimes we do not have time to call the OS.*

*The OS is not the only entity that talks to the hardware. (It is not all the time)*

*The user program can possibly talk to the hardware. It often happens because of the performance reason.*

OS is like a software that manages other software. The OS acts like an abstraction for other running processes.
Abstraction makes things simpler and efficient.


There are different ways to structure an OS. (Architecture)

## Monolithic
Kernel:
- One big special program
*Put everything into one, put all the different component into one kernel*

*Despite its so big, it is still able to develop proper abstraction. Community built*
- Traditional approach taken by:
Unix, Windows

Advantages:
- Well understood
*Allowed changes to modify the system into what we need*

- Good performance
*All the components can talk to each other efficient*

Disadvantages:
- Highly coupled components
- Usually devolved into very complicated internal structure

## Microkernel
Kernel is:
- Very small and clean
Anything that can be taken out is taken out
- Only provide basic and essential features
    - IPC (Inter-process communication)
*This is important because several parts were taken out, so this process is needed for the OS to talk to other parts of system that is not part of the OS.*


Advantages:
- Kernel is generally more robust and more extendible
- Better isolation and protection between kernel and high level services

Disadvantages:
- Lower performance
*But we have to involve the kernel to talk to other component so efficiency is not good*



## Extra

### Exokernel: the smallest kernel
### Split kernel:
Physically split amongst several machines

# OS as a program
OS is also known as the kernel, a program with special features.
The OS has to deal with hardware, interrupt handles and device drivers.
Provides system call interfaces and deal with hardware issues

Machine dependent HLL
ifdefs 

This is the architecture dependent code

Machine dependent assembly code

# Virtual Machines
A vm is a software emulation of hardware.
OS assumes total control of the hardware. But sometimes we want to run multiple OS at the same time on the same hardware. The virtual machine allow us to contain the errors. 

Instead of having a real hardware, we can expose some fake hardware and trick the OS to think that it is real hardware.
The real hardware being exposed must seem very similar to the real hardware.

Hypervisors
Exposes the fake hardware to the OS

Type 1
- Provided individual virtual machine to guest OS
Insert 40


Type 2

- Acts as the hardware for guest OS
- Runs in host OS
- Guest OS runs inside VM

(Insert 41)
