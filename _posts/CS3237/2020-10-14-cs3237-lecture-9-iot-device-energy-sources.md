---
layout: post
published: true
title: 'CS3237 - Lecture 9: IoT Device Energy Sources'
---
# Battery Characteristics

## Requirements
- The size matters
- Physical size:
	- Typically miniature assemblies having a battery compartment, socket or wiring harness for connection
- Operating environment
	- Wide range of conditions from indoor outdoor etc
    - Operating environement dictates whether the abttery options are limited to thsoe having industrial automotive or commercial temperature ratings

## Selection
- Meets min perf objectives
- Will last the intended life
- If batt replacement is expected, ensure that the battery can be replace with minimal expense and difficulty and in complicance with disposal regulations

## Specification terms
- Nominal Voltage: The reported or reference voltage of the battery also sometimes thought of as the normal voltage of the battery
- Cut off volatage: The min allowable voltage, this define the empty state of the battery
![CS3237-9-1.PNG]({{site.baseurl}}/img/CS3237-9-1.PNG)

## Battery Capacity
- Battery Capacity is specified in AH
- Coulumb is the equivalent of one ampere- second. COnversely an electric current of A represents 1 C of unit electri charge carriers flowing past a specific point in 1s
- The charge in columbs Qc is equal to the charge in ampere- hours Q(ah) times 3600
- 1AH = 3600C

## Power capacity
- THe amount of current can draw is limited
- Sometimes the battery is not capable of providing 1AH of current and not expected to last less than expected
- The default discharge rate is specified as C rate

## C rate 
- 1C rate means that the discharge current will dischage the entire battery in 1 hr
- FOr a bettery with a cap of 1-- amps, this equates to a discharge current of 100 Amps
- 5C rate for this battery would be 500Amps
- C/2 rate for thsi battery would be 50 Amps

## Battery specification terms
- Capacity or Nominal capacity: The coulometric capacity, the total AMP hours available when the battery is dischaged at a certain discharged current from 100 percent state of change to the cut of voltage
- Capacity is calculated by multiplying the dischaged current 
- Capacity decreases with increasing C-rate

![CS3237-9-2.PNG]({{site.baseurl}}/img/CS3237-9-2.PNG)


## Simplified Battery life model
![CS3237-9-5.PNG]({{site.baseurl}}/img/CS3237-9-5.PNG)

- If its 2A, the Capacity will be lower
- If its .1 A the capactity will be higher
- Discharging at higher rates removes more power from the battery
- Peukert effect helps predict the life of a battery where the capacity of a battery decreases at a different rate as discharge increases

The larger the exponenet the battery is, the lesser time the battery surivives

![CS3237-9-6.PNG]({{site.baseurl}}/img/CS3237-9-6.PNG)


# Slides
<iframe src="https://drive.google.com/file/d/1uRMjDWDpvft4B2oA1-9A3Ma1r0WHZeaQ/preview" width="640" height="480"></iframe>
