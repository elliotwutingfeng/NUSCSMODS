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

### Example
![CS3237-9-8.PNG]({{site.baseurl}}/img/CS3237-9-8.PNG)

- 20C * 3000MAh = 60A (Charge:  60coulombs of electrons are passing through the wire in 1 second)

> - c-rate = 1 means you can use the battery for 1h
> - 20C means 20x the power
> - 3000mah: it means you can run the battery at 3000ma for 1h


## Battery specification terms
- Energy Density
- Dept of discharge
- Cycle life
![CS3237-9-9.PNG]({{site.baseurl}}/img/CS3237-9-9.PNG)


# Energy harversting
- Many Iot edge devices are battery powererd
- Matterials needed for batt production are scardes
- Process where the energy is derived from external resources


Example:
- Light
- Thermal
- Radio
- Kinetic
- Chemical
- Atmospheric 
- Hydro

![CS3237-9-10.PNG]({{site.baseurl}}/img/CS3237-9-10.PNG)

- Interface circuit: Converts the energy to a form thats acceptable
- Sometimes there are no energy storage and the power goes directly to the load
- It is important to dimension the energy source and the storage

	
## Solar Harvesting
- Energy from light
- Photodiodes can be used in large quantities to build solar array
- Capacity of energy generation is a function of the area of the solar array
- Indoor solar generation is not as efficient

## Piezo Mechanicals Harvesting
- Mechanical strains can be converted to energy through motion, vibration and even sound
- These harvesters could be use in smart roadways an infrastructure to harvest and change system


# Slides
<iframe src="https://drive.google.com/file/d/1uRMjDWDpvft4B2oA1-9A3Ma1r0WHZeaQ/preview" width="640" height="480"></iframe>
