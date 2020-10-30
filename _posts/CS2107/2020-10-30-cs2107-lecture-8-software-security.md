---
layout: post
published: true
title: 'CS2107 - Lecture 8: Software security'
---
# Overview

Requirements:
	- Correct
    - Efficient
    - Secure

Targeted/Intended program functionality vs possible behavior:
- A program may behave beyond its intended functionality!

![CS2107-8-1.PNG]({{site.baseurl}}/img/CS2107-8-1.PNG)


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
> - The location is stored somewhere

> Where are the function's arguments and local variable stored?
> - On the stack

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


Function call:
![CS2107-9-3.PNG]({{site.baseurl}}/img/CS2107-9-3.PNG)

1. When test(5) is called, some values are pushed onto the stack
	- Parameter
    - Return address
    - Prev frame pointer
    - Local variable b
2. The control flows jump into the code of test
3. Execute test
4. After test is completed, the stack frame is popped from the stack
5. The control flows jumps into the restored return address


## Control flow integrity

Treating code as data:
- Call stack stores a **return address** as data in memory
- Instruction itself is stored as data in memory
- Flexibility of treating code as daata is good but many security issue
- Attacker could c**ompromise a process execution integrity** by 
	- modifying the process code 
    - Modifying the control flow
- It is difficult for the system to distinguised those malicious pieces of code from benign data

### Notes on memory integrity
- Not so easy to comporomise memory
- Some restrictions:
	- The attacker can only write to a small number of memory 
    - Can write a seq of consecuitve bytes

# Attacks on software

## Integer overflow
- The integer arithmetic in many programming language are actually modulo arithmetic
- Suppose a is a single byte unsigned integer. 
	In the following C or java statements, what would be the final value of a?
    	- a = 254
        - a = a +2
- Its value is - since the addition is done in mod 256
- Hende the following predicate is not always true
	- a < a + 1

## Data/string representation and security
- Different oarts if a program/system adopts different data representations
- Inconsistencies could lead to vulnerability
- String is a very important data representation type:
	- It has variable length 
    - How can we represents a string?

### String representations
- In C, printf() adopts an efficient represention:
	- The length is not explicitly stored
    - The first occurance of the null character (Byte with value 0) indicated the end of the string, thus implicity giving the length
    
![CS2107-9-4.PNG]({{site.baseurl}}/img/CS2107-9-4.PNG)


#### Null Byte Injection
- A CA may accept a host name containing null character
- For example: luminus.nus.edu.sg\0.attacker.com
- The verifer who use both string representation convention to verify the cert might be vulnerable

ATTACK:
1. The attacker registered the following domain name, and purchased a valid certificate with the domain name from some CA: luminus.nus.edu.sg\0.attacker.com
2. The attacker set up a spoof Luminus website on another web server
3. The attacker directed a victims to the spoofed web server (e.g by controlling the physical layer or social engineering)
4. When visiting the spoofed web server, the victim's browser:
	- Find the web server in the certificate is valid: based on the non NULL termination representation
    - Compares and display the address as luminus.nus.edu.sg: based on NULL termination represesntation
    
![CS2107-9-5.PNG]({{site.baseurl}}/img/CS2107-9-5.PNG)
![CS2107-9-6.PNG]({{site.baseurl}}/img/CS2107-9-6.PNG)

Comparision: Normal web spoofing attack
- What if its jus normal web spoofing attack scenario?
- Even if the attacker manages to redirect the victim to the spoofed webserver a careful user would notice that either
	- The address displayed in the browsers address bar is not luminus
    - The address displays but TLS/SSL authentication protocol reject the connection
> Hence the attack on the previous slide, is much more dangerous: It can trick all browsesr user!

#### UTF-8 Character exploits
UTF-8 is a character encoding capable of encoding all 1m valid code points in unicode using one to four 8 bit bytes

Variable length encoding: Code points that tend to occur more frequently are encoding with lower numerical values thus fewer bytes are used.


![CS2107-9-7.PNG]({{site.baseurl}}/img/CS2107-9-7.PNG)
![CS2107-9-8.PNG]({{site.baseurl}}/img/CS2107-9-8.PNG)

There is an inconsistency
between
- Character verification process
- Chaaracter usuage: Operation using the character

> Browser actually accept different types of representation for the backslash charac


Potential problem:
- Files are typically organised inside a directory


- Client can be any remote piblic user
- Original intention: Client can retrieved only files under the directory
- But attacker might send this string: `../cs2107report.pdf`
- This would be read by the server as `/home/student/alice/public_html/../cs2107report.pdf`
- Violates the intended file access containment
- Blacklisting based filtering might be useless due to the flexibility of the encoding
> TO prevent thism server ma add an input validation to ensure that `../` never appears as substring


Example: IP Address
![CS2107-9-9.PNG]({{site.baseurl}}/img/CS2107-9-9.PNG)


Vulnerable checks:
1. Get string s from user
2. Extract 4 int from string s, (a,b,c,d)
	- If s doesnt follow correct inputm then quit
3. call BL() to check that abcd is not in the black list, else quit
4. Let ip = a * 2^24 + b * 2^16 + c * 2^8 + d  where ip is 32 bit integer
5. Continue processing with filtered ip


#### Security guidelines
1. Never trust user input
2. ALways convert to standard representation immediately
3. Do not rely on the verification check done in the application
4. try to make use of the udnerlying system access control verification
## Buffer overflow

### C/C+ and memory access
- ALlows the programmers to manage the memroy: Pointer arithmetic, no array bounds chekcing
- Flexibility is useful but prone to bugs which in turns lead to vulnerability

### Buffer Overflow/Overrun
- The previous example illustrates buffer overflow
- A data buffer: "A contiguous region of memory use to temporarily store data, while its is being moved from one place to another" (Like a array of characters)
- In general, a buffer overflow referes to a situation where data is written beyond a buffer boundary
- `strcpy()` is prone to overflow

> Avoid strcpy

### Stack smashing 
- Stack overflow
- Special case of buffer overflow
- return address is modify and the execution control flow will be changed
- COuld also inkect the attackers shell code into the process memory and execute the shell code

#### Example
Vulnerable code:
![CS2107-9-10.PNG]({{site.baseurl}}/img/CS2107-9-10.PNG)

- If more characters are copy, the value will get over flow and the return address will get overwritten

![CS2107-9-11.PNG]({{site.baseurl}}/img/CS2107-9-11.PNG)


## Code/script injection

- Mixing code and data is unsafe
- Many attacks inject malicous code as data which will then gets executed by the target system
- Considered SQL attack

### SQL and Query 
- SQL is database query language
- Consider a database (Which can be viewed as table): each column/field is associated with an attibute
- Also allows variable:
	- e.g a script may first get the user's inputs and stores it in the variable $userinput and subsequently runs:
    SELECT * FROM Client WHERE name = '$userinput'

#### Example



## Undocumented access points
# Defence and preventive measures
