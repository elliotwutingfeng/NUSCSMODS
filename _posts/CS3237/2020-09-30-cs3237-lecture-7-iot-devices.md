---
layout: post
published: true
title: 'CS3237: Lecture 7 - IOT Devices'
---
# IOT Architecture

#### Components
- Uniquely identifiable embedded system connected with the internet infrastrcuture
- IOT Devices collect data through sensors
- The data is sent to the internet through the gateway
- Things and Gateway are generally considered as the edge of the internet
- Data analytics takes place in the cloud
- Following anayltics actuator commands might be sent

> Why do anayltics on the IOT device rather than the cloud
>
> - Security
> - Time
> - Cost



![CS3237-7-1.PNG]({{site.baseurl}}/img/CS3237-7-1.PNG)

- Sensor reads in analog data that is converted to digital forms using analog to digital converter
- Actuator receives digital signal that is converted to electrical or electromechnical signals through DAC
- Controller contains a processor
- Controller is connected to the internet


#### Example
![CS3237-7-2.PNG]({{site.baseurl}}/img/CS3237-7-2.PNG)
- 10 sensors

## Sensor
- Connect the analog world to digital
- Each IOT sensor collects a stream of time correlated data that must be transmitted securely, possibly anaylsed and possibly stored
- Value of IOT is in the data in aggregate from multiple sensors
- Sensor data may not be always be reliable and sensors can fail in field

![CS3237-7-3.PNG]({{site.baseurl}}/img/CS3237-7-3.PNG)

## Digital input
- Example: On off Switches
- Push button: Reverse for normally closed switch
- Push on switch: Must be depressed again too release 

## Contact bounch of mechanical switch
- Contact bounce: Mechanical switches do not make clean transition between on off position, makes/break contact multiple times for tens of millisecons
- Microcontroller is fast and can recognised each swithc bound
- Debouncing solution:
	- Hardware debounce circuit
    - Software technique: Insert delay
    
## Analog sensors
- Converts the analog data to digital
- Examples
	- Temperature sensor uses the fact that as the temp increases, the voltage across a diode chantges at known rate
    - Flex sensor provides a change in resistance for a change in sensor flexture
![CS3237-7-4.PNG]({{site.baseurl}}/img/CS3237-7-4.PNG)

## Continous time signal
- A continuous time signal is defined over all instance of time
- A function of time (The real number) to the co-domain X

## Discrete signal
- Sequence or series of signal values defined in discrete points of time
- THe distance in time between each point of time is the time step

![CS3237-7-5.PNG]({{site.baseurl}}/img/CS3237-7-5.PNG)

## Digital Signal: Quantisation 
- Digital signal is a discrete signal for which not only the time but also the amplitude has been made discrete
- ADC samples and quantizes an analog signal to digital signal

![CS3237-7-6.PNG]({{site.baseurl}}/img/CS3237-7-6.PNG)

## ADC (Quantization and encoding)
- Input boltages are typically mapped in range of 0-5 volts
- b bit allows to divide the input signal range into 2^b different quantization level
- The more bits we have available, the higher resolution: (volatage span)/2^b = (vref (hih) - Vref(low))/2^b

## Output devices and actuators
- Digital Output
	- Example: LED
    - Informs the presence of logic 0 or logic 1 at a specific pin of a microcontroller
- Analog actuators
	![CS3237-7-10.png]({{site.baseurl}}/img/CS3237-7-10.png)


## Pulse width modulation (PWM)
- Method to create an analoig signal from a digital processor
- The main idea is to keep the signal high for an amt of time proportianl to the aplitude of the required analog sigals

![CS3237-7-8.PNG]({{site.baseurl}}/img/CS3237-7-8.PNG)


Example
![CS3237-7-7.PNG]({{site.baseurl}}/img/CS3237-7-7.PNG)
- During the period, the pulses are on for a certain period of time
- What is different is how many percentage of the time is the pulse on.

![CS3237-7-9.PNG]({{site.baseurl}}/img/CS3237-7-9.PNG)

## Sensor/Actuators interface with microcontoller
- Sensor data has to be processed and transmitted
- Sensor connect to a microcontller through established I/O interfaces and communication system
- Video system need much faster I/0 such as MIPI, USB, UCB expresee

## I2C communcation protocol
- Reqyures 2 wires
- Serial interace
- Sending one bit at a time
- Use for short distance communication

![CS3237-7-11.PNG]({{site.baseurl}}/img/CS3237-7-11.PNG)

# Sensor
![CS3237-7-12.PNG]({{site.baseurl}}/img/CS3237-7-12.PNG)

- Ambient light sensor
- Infrared Tempt sensor
- Humidity and temperature sensor
- Barametric pressure sensor
- Motion sensor
- 3D accelerometer and gyroscope
- Bungee Jump Acceleration

# Summary
- IOT device consist of sensor actuators and microcontroller
- Variery of sensor connect to the cyber world to the physical world
- ADC And DAC perform transformation between analog and digital


# Slides
<iframe src="https://drive.google.com/file/d/141abjr0nVvkRAYzFvwBnKNhtvcuVWDLD/preview" width="640" height="480"></iframe>
