---
layout: post
published: false
title: 'CS2107 - Lecture 8: Software security'
---
# Overview

Requirements:
	- Correct
    - Efficient
    - Secure

Targeted/Intended program functionality vs possible behavior:
- A program may behave beyond its intended functionality!



### Possible Security Problems
- Insecure implementation:
	- Many Programs are not implemeted properly, allowing attacker (The person who invokes the process)
    - Deviate from the programmer's intents
- Unanticipated input:
	- The attacker may supply inputs in a form that is not anticipated by the programmer which can unintendedlu cause process to:
    	- Access sensitive resources
        - Execute some injected code; or 
        - Deviate from the original intended execution path
> Either way, the attacker manages to elevate its privilege

Sample:
- Buffer overflow:
	- Morris worm
    - Code red worm
    - SQL Slammer worm
    - Various attacks on game consoles so that unlicense software can run without the need for hardware
- SQL injection
- Integer overflow

Root causes of security Problems
- Functionality: Still the primary concern during design and implementation
	- Security is a secondary goal
    - Features pays the bills (Typically)
- Unavoidable human mistakes:
	- (lack of) awareness of secuirty problems
    - Careless programmers
- Complex modern computing system:
	- Many of the bugs are very simple and seem easy to prevent, but programs for complex system are large
	- Large attack surface as wells

# Computer architecture background
## Code vs data, program counter
Modern computers are based on the von neumann computer architecture:
	- The code and data are stored together in the memory
    - There is no clear distinction of code and data
    - This is in contrast to the Harvard architecture, which has hardware components that separately store code and data

Serious implication:
- Programs may be tricked into treated input data as code: Basis for all code-injection attacks!


## Control flow
- The program counter (Instruction pointer):
	- A register (ie small & fast memory within the processor) that stored the address of the next instruction
- After an instruction is completed, the processor fetches the next instruction from the address stored in the program counter
- After the next instruction is fetched, the program counter automatically increase by 1 (Assuming a system with fixed-length instruction)
- During execution, besides getting incremented, the program counter (PC) can also be changed, for example*, by:
	1. Direct Jump:
    	The PC is replacded with a constant value specified in the instruction
    2. Indirect Jump:
    	The PC is replaced with a value fetched from the memory or stored in a general purpose register (Note that there are many different forms of indirect jump)
        
        
## Stack
- Function: Break code iunto smaller pieces
	- Can be called in many program location

> How does the program knows where it should continue after it finished?

> Where are the function's arguments and local variable stored?

### Call stack
- Call stack: A data structure in the memroy (Not in a sep hardware) that stores important infomation of a running processes
- Last in, first out (LIFO): with push(), pop(), top() operations
- The location of the top element is referred to by the stack pointer
- During a program execution, a stack is used to keep tracks of:
	- Control flow infomation: i.e address
    - Parameter passed to functions
    - Local variables of function

- Each call of a function pushes an activiation record (stack frame) to stack, which contains: passed parameters, return address, pointer to the previous stack frame, adn function local variables

> This is called call stack

## Control flow integrity

# Attacks on software
## Integer overflow
## Data/string representation and security
## Buffer overflow
## Code/script injection
## Undocumented access points
# Defence and preventive measures
