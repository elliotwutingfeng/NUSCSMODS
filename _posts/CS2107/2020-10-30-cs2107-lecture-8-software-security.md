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
![CS2107-8-17.PNG]({{site.baseurl}}/img/CS2107-8-17.PNG)

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
> - The location is stored on the call stack

> Where are the function's arguments and local variable stored?
> - On the call stack

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


![CS2107-9-11.PNG]({{site.baseurl}}/img/CS2107-9-11.PNG)

- If more characters are copy, the value will get over flow and the return address will get overwritten
- It will also can jump to the executed code section

![CS2107-9-12.PNG]({{site.baseurl}}/img/CS2107-9-12.PNG)

## Code/script injection

- Mixing code and data is unsafe
- Many attacks inject malicous code as data which will then gets executed by the target system
- Considered SQL attack

### SQL and Query 
- SQL is database query language
- Code can be put as a string and executed in runtime
- Consider a database (Which can be viewed as table): each column/field is associated with an attibute
- Also allows variable:
	- e.g a script may first get the user's inputs and stores it in the variable $userinput and subsequently runs:
    SELECT * FROM Client WHERE name = '$userinput'
    
> This can happen in login page, where the name is selected by the user

#### Example
In the example of the login page, web developers will take the user input and use the `SELECT` search query to retrieve the data
- Attack can do this
	- Bob' OR 1=1 --`
    - this becomes `SELECT * FROM client WHERE name = 'bob' OR 1=1 --`
    - All rows in this client table will be return this this case


## Undocumented access points
- For debugging, many programmers insert undocumented access point to inspect states
	- Press certain key combo, values of certain variables will be display
    - Certain input string would branch to debug mode
- These access points may mistakenly ramin in the final production system providing backdoors to the attackers
- A backdor: A covert method of bypassing normal authentication
- Such access points are easter eggs
	- Some are fun
    - Some are put there by unhappy programmers
- Important: Logic bombs, easter eggs, backdoors

# Defence and preventive measures
- Many bugs and vulnerability are due to programmer innorance
- It is diffucult to analysis a program to ensure that its bug free
- THere is no fool proof method

## Input validation and using filtering
### Filtering
- Input must follow expected format
	- Length
    - Cannot contain certain meta characters
    - Does not contain negative numbers
- Filter the input or validate it 

Problems:
- Difficult to ensure filter is complete
	- e.g UTF: Input validation intend to detect the substring
    - There are multiple representations of "../" that the programmer is not afraid of
    - A filter that completely blocks all bad inputs and accepts all legitimate inputs is very difficult to design


Approaches:
1. White list
	- List of items are allowed to pass
    - Regex
    - Bad: Some legitamate input might be block
2. Black list
	- A list of items that are known to be bad and has to be rejected
    - To prevent SQL injects, if the input contains meta characters, reject it
    - Malicious input may be pass

> Which is more secure?

### Safer functions
- Avoid function that cause problems
- For example, repolace strcpy with strncpy
- There still might be a vul:
	- combine strlen and strncpy

### Bounds check and type safety
Bounds check:
- Some programming language perform bounds checking at run time
- Checks upper and lower bounds
- process halt if both checks fail
- reduces efficiency but prevent buffer overflow

Type safety:
- Check to ensure args in operation get are always correct
- e.g, if a= b but a is 8 bit while b is 64, type is wrong
- Check done in runtime(dynamic type) or compiled (static type)


## Memory protection
## Canaries
- Secret value inserted at carefully selected memory location at runtime
- Checks are carried at at runtime to ensure that the values are not being modified
- Canaries can detect overflow such as stack overflow:
	- Typical bufferoverflow, consecutive mem location have to be over ran but canaries would be modified
- Keep the values secret: If attacker knows, they can write the secret value to the canary while overrunning it
![CS2107-9-14.PNG]({{site.baseurl}}/img/CS2107-9-14.PNG)

- If the buffer was overflow, the canary would be overwritten

#### Another example
![CS2107-9-15.PNG]({{site.baseurl}}/img/CS2107-9-15.PNG)
- Buffer overflow occurs at strcpy
- `./program-too-wsp aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa`

If compiled with stack protector:
- Stack smashing
- Function exiting
- Aborted (core dumpted)

Without stack protector:
- Function exit
- Seg fault but, the program might jump to a unwanted address

#### Example 2

![CS2107-9-16.PNG]({{site.baseurl}}/img/CS2107-9-16.PNG)


- `./program-too-wsp aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa`

If compiled with stack protector:
- Stack smashing
- Function exiting
- Aborted (core dumpted)

Without stack protector:
- Function exit
- Seg fault but, the program might jump to a unwanted address
- main() is exiting is shown

## Memory randominisation
- ASLR (Address space layout randomisation) is a prevention technique that helps decrease the attacker's chance
- Randomly arranges the address space position of key data areas of a process including:
	- THe base area of the executable and the position of the stack, heap and libraries

## Code inspection
- Manual checking: Manually check the progranm is tedious
- Automated: Some automation and tools are posible
- Taint analysis:
	- Variables that contain input from potential malicious users are labeled as **sources**
    - Critical functions are labeled as **sinks**
    - Taint analysis checks whether any of the sinks arguments could potentially be affected by a source
    - Source = user input
    - Special check: Carried out
    - Taint analysis can be static or dynamic
## Testing
- Vulnerability can be discovered via testing
- Types:
	- White box testing: Tester has access to application source code
    - Black box: Does not have access to source code
    - Grey box: Combination above, reverse engineered binary/executable
- Security testing attempts to discover intentional attack and hence would test for inputs that are rarely occured under normal circumstance
- Examples: Long name, names containing numeric values, string containing meta characters
- Fuzzing is a technique that sends the malformed inputs to discovered vulnerability:
	- Some techniques are btter then this for random inputs
    - Fuzzing can be automated or semi auto
    
    
## Principle of least priviledge
- When writing a prob, be conservative in elevating the priviledge
- When deploying software system, do not give the users more access rights than neccessary and do **not** activate unnecesarry options
	- Like setUID
> Terminology: Hardening
> - hardening is usually the process of securing a system by reducing its surface of vulnerability, which is larger when a system performs more functions;

# Patching: Up to date
- Life cycle of vulnerability:
	1. Discovereed
    2. Code fix
    3. Revised tested
    4. Patch made public
    5. PAtch applied
- Sometimes vulnerability can be announced without the techniqcal details
- When patch release, the patch can be useful to attackers too: Inspect the patch and derive the vulnerability
- Funnily, sometimes the number of successful attack increase when a patch is made
- Cruicial to apply timely

- Critical system: DOnt apply patch immediately before rigorous testing
- Patches might affect the applications and thus affect an org operation


![CS2107-9-17.PNG]({{site.baseurl}}/img/CS2107-9-17.PNG)

# Slides
<iframe src="https://drive.google.com/file/d/12bpGSoVRszagt61E_B8WV2tyyGe1GTBv/preview" width="640" height="480"></iframe>
