---
layout: post
published: true
title: CS4222 - Contiki Lab Set Up
---
# Make file
 
 Sample:
```

```

file name: Makefile

Command:
`make TARGET=srf06-cc26xx BOARD=sensortag/cc2650 hello-world.bin
CPU_FAMILY=cc26xx`

Note: Change hello-world to the name of the c file.


# UNIFLASH CONFIG
1. Set up
![CS4222-lab-1.PNG]({{site.baseurl}}/img/CS4222-lab-1.PNG)

2. Erase Flash
Setting&Utilities > Erase entire Flash

3. Load Bin

# Reading output

`cat /dev/ttyACM0`