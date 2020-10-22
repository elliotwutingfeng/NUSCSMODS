---
layout: post
published: false
title: 'CS2107 - Lecture 7: Access control'
---
# Overview of layering model in conmputer design
#### Layers in computer system


#### Comparing to layers in communication network
Network:
- The boundary is more well defined
- Infomation/data flows from the topmost layer down to the lowest layer and is transmited from the lowest layer to the topmost layer
- A concern of data confidentiality and integrity

Computer system:
- The boundary is less well defined
- Every layer has its own "processes" and "data" (although ultimately, the raw processes/data are handled by hardware)
- The main security concern is about access to the process and memory storage
- Hence beside data confidentiality and integrity (E.g password file), there is also a concern of process "integrity" whether it deviates from its original path

#### Attackers and system's layer
- Suppose an attacker sneaks into layer 1
- The attacker must not be able to directly manipulating object/data and processes in more priviledge Layer 0
- Note that is is very difficult to ensure this requirement

## Security Mechanism
- It insightful to figure out at what layer a security mechanism/attack resides
- A lyer based security mechanism should have a well defined security perimeter/boundary


- Important design consideration:
	- How to prevent attacker from getting access to a layer inside the boundary
    - E.g: SQL injection attacks target at the SQL DBMS.
    - The OS password management: Remain intact even if SQL injection attack
- Possible application takes care of its own security (Self-secure):
	- E.g application always encrypt its data before writing them to file system
    - Even if access control of the files system is compromised (e.g malicious user can read someone else files), the confidentiality of the data will still be preserved

# Access control model
- Required in computer system, infomation system and physical system
- Different application domains have different requirements/interpretation
- Examples of application domain:
	- OS
    - Social media
    - Documents in an organisation (Document can be classified as restricted, confidential, secret,etc)
    - Physical access to different part of the building
- The access control model/system gives a way to specify& enforce such restriction on the subject, objects and action

> Acess control is about selective restriction of access to a place or other resource

## Principal/Subject, operation, object
- A principal wantss to access an object with some operation
- The reference monitor either grants or denies the access
- e.g
	- Luminus: A student wants to submit a forum post
    - Luminus: a student wants to read the grade of another student
    - File system: A user wants to delete a file
    - File systemL A user Alice wants to change a file's mode so that it can be read by another user named Bob
- Principals vs Subjects
	- Principal: the human users
    - Subject: The entities in the system that operates on behalf of the princpial, e.g process, request
- Access to object can be classified to the following:
	- Observe:	e.g reading a file
    - Alter: e.g writing a file, deleting a file, changing properties
    - Action: Executing a program
## Object access rights and ownership
- Discretionary access control (DAC): The owner of the object decides the rights
- Mandatory access control (MAC): A system wide policy decides the rights, which must be followed by everyone in the system must follow

> Which file system is UNIX

## Access control representation
- Access control matrix: Matrix of principals vs objects
- The access control matrix can be represented in 2 way: Access Control List (ACL), or capabilities
- Access control List (ACL): store the access rights to a particular object as a list
- Capabilities: 
	- A subject is given a list of capabilities, where each capability is the access rights to an object
    - A capability is an unforgeable token that gives the possessor certain rights to an object

## Drawbacks of ACL and Capabilities
ACL:
- Difficult to get an overview of which objects that a particular subject has access rights to
- Example: In UNIX, the system admin wants to generate the list of file that the user ALICE has 'r' access to. How to generate this list?

Capabilities:
- Difficukt to get overview of the subject who have access rights to a particular object
- E.g Given a particular object, which subject can access this object


Both methods:
- The size of the list can still to be too large to manage
- Hence we need to find some way to simplify the representation
- One simple method is to group the subjects/objects and define the access rights on the defined groups
- Need intermediate control

## Intermediate control: Group
In UNIX file permission, the ACL specifies the rights for the following user classes:
	- User (owner)
    - Group (The owner's group)
    - Other (world)
- Non-owner subject in the same group: have the same access rights
- Some system demand that a subject is a single group, but some system don't put such restriction

## User and groups: Illustration

## Intermediate control: Protection Rings
- Here each object (Data) and subject (process) are assinged a number
	- If a process is assigned a number i: it runs in ring i
    - If an object is assigned a number i:  Its accessible in ring i
    - The smaller the number is the more important: We can call processes with lower ring number as having higher priviledge

# Access control in UNIX/Linux
- Objects of access control includes:
	- Files
    - Directories
    - Memory devices
    - I/O devices
- All resource are treated as file

## User and groups
- Each users:
	- Has unique user/login name
    - Has numeric user indentifier(UID): Stored in /etc/passwd
    - Can belong to one or more groups:
    	- The first group is stored in /etc/passwd
        - Additional groups are stored in /etc/group
- Each groups:
	- Has a unique group name
    - Has a numeric group identifier (GID)
    
Main purposes of UIDs and GIDs
	- To determine ownership of various system resources e.g files
    - To determine the credentials of running processes
    - To control the permissions granted to proccesses that wish to access the resource
## Principals
- User indeities and group identities
- Infomation of the user accounts are stored in the password file /etc/passwd
- Additional group infomation of a user is stored in /etc/group
- A special user is the superuser with UID 0 and usually the username root
	- All security checks are turned off for root

#### Remarks
- The file is made world reable because some ifno in etc/passwd is needed by non root processes
- Note that in the older version of UNIX, the location of the "*" was the hashed password H(pw)
- The availabilitiy of the hashed password allows attackers to carry out an offline password guessing
- Since password are short, exhaustive search are able to get many password
- Prevention: replaced by `*` and the actual password is stored somewhere else and is not world readable

> Location might be in the shadow password file


### The shadow password file
- Fields of entry seperated by `:`
	- Login name
    - hashed password
    - Date of last password change
    - Minimum password age
    - Max password age
    - Password warning period
    - Password inactivity period 
    - Account expiration date
    - reserved field
- The second filed (hashed password) has the following format: `$id$salt$hashed-key`
- id: ID of the hashed method used
- Salt: Up to 16 char drawn from the set
- Hashed key : Hashed of the password

## UNIX/LINUX subjects
- Subjects: Processes
- A new process: Created by invoking an executable file or due to a fork by existing process
- Each proccess has a process ID (PID):
	- Use the command ps aux or ps -ef to display a list of running processes

## Selected issues: Search path
- When a user types in the command to execute a program say "SU" without specifiying the full path, {INSERT}
- Program is search through the directories specified in search path
- `echo $path`
- Search stops when name found and program will execute

#### Attacker
- Attacker store malicious program in directory in the beginning of the search path
	- Has common name: `su`
    - User execute `su`
    - Malicious program invoked instead
- Prevent: Specify full path

> Avoid putting the current directory "." in the search path

## Files
### FIle and file system permission
### Changing the file permission bits

#### Chmod
#### Symbolic mode notation
#### Octal mode notation
#### Additional
- Directory permissions:
	- r: ALlows the contents of teh directory to be listed if the x attribute is set
    - w: Allows files within the directory to be created, deleted, renamed if x is set
    - x: Allows directory to be entered
- Special file permission:
	- set-uid: Process effective user ID of is the owner of the executable file (Usually root) rather than the user running the executable
    - set-gid: The process effective group id is the group owner of the exe file
    - Sticky bit: If dir has this bit set, file can only be deleted by the owner of the file, the directory or by root

## Objects and their access control
- Each filke is owned by user and group
- Each file is associated with 9bit permission
- When non root user wants access the file:
	1. If user is owner, the permission bit for owner decides the access rihgts
    2. If user not owner, but GID owns the filem the permission bits for group decide the access rights
    3. If user is not owner nor member of the group that owns the file, the permission bits for other decide

> Owner of file or superuser can change permission bits

## Controlled invokation
- Certain resources can be access only by super user
	- Listening at trusted port
    - Accessing shadow file
- It is not advisable to promote user status to superuser


> But sometimes non root need access the resource (change password)

Control invokation provides a predefine set of operation in a superuser mode and the non-root user can then run those operation with superuser mode

- OS supports this solution using the set-UID bit of an exe

Example:


The `s` bit indicates that the privilege is escalated to the file owner (root) while user is running the processes

# UNIX/Linux: Elevated privilged (Contolled invocation)

## Process credentials and set user ID
- Process is a subject: Has PID
- Process associated with process credentials:
	- Real UID
    - Effective UID
- Real UID inherited from user who invokes the process: Identifies the real owner of the processes
	- e.g if user is ALICE then process real UID is alice
- For process created by exe file:
	- if set-uid is disable (permission bit is x), then process effective UID is same as real UID
    - if set-uid is enable (permision bit is s), then process effective UID is inherited from the UID of the file's owner
