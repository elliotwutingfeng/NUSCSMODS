---
layout: post
published: false
title: 'CS2105 - Lecture 10: Multimedia Networking'
---
> We are going back to application and transport layer.

# Mutlimedia networking Application

#### Why learn about this?
Video is predominant on the internet

- Popular services
- All delievers as OTT

> OTT: Over the top - Video services are delievered on top of the internet
ISP does not deliever what you get from the internet

## Multimedia: Audio

- Analog audio signal smaple at constant rate
   - Telephone: 8000 samples/sec
   - CD Music: 44100 sample/sec
   
- Each sample quantized
   - 2^8 = 256 possible quantized values
   - Each quantized values represented by bits
   
![2105_10_1.PNG]({{site.baseurl}}/img/2105_10_1.PNG)

> Converting bits back to analog can cause some quality reduction

- ADC: Analog to digital converter
- DAC: Digital to analog converter

> Humans are more sensitve to certain frequency (low) thus we can remove the higher frequency and record our audio in lower bit-rates

## Multimedia: Video

- Sequence of images displayed at a constant rate
- Digital image: Array of pixels (Each pixel is a bit)
- Coding: Use redundancy within and between images to decrease number of bits used to encode image
   - Spatial (Within image) 
   - Temporal (From one image to next)

1. CBR: (Constant bit rate) - Video encoding rate fixed

-> Better quality

2. VBR: (Variable bit rate): Video encoding rate changes as amount of spatial temporal coding changes

-> Constant visual quality

## Multimedia networking: 3 Application types

- Streaming, stored: Audio, video
  - Streaming: Can begin playout before downloading entire
  - Stored(At server): Transmit faster than audio/video will be rendered (Theres buffering)
- Conversational (Two way live) voice/ video over IP
  - Interactive nature of human to human conversation limits **delay tolerance**
  - e.g Skype, zoom
- Streaming live (One way live) audio, video
  - Live sporting event ( soccer, foootball)

# Streaming stored video

![2105_10_2.PNG]({{site.baseurl}}/img/2105_10_2.PNG)

1. Data is produce and captured at a time
2. Stream the data in the similiar way
3. Data arrives at the client in the same way
4. Sent to the decoder and

> Streaming at the (2) later time, client playing out early part of video while server still sending later part of video

## Challenges

- Continuous playout constraint: Once client playout begins, playback must match original timing
   - But network delays are variable (jitter) so we need a client side buffer to match playout requirements
- Other:
   - Clinet interactivity: pause, fast-forward, rewind, jump through videos
   - Video packets may be lost, retransmitted

More realistic:

1. There might be variable network delay between sending the packets
2. The staircase might be uneven
3. Play back will be stalled if the packet has not arrived.
4. Including a buffer at the client side: Will ensure that we have the packets before starting the playback
5. We can see if there is no problems if the blue curve is not intersectted by the black curve

![2105_10_3.PNG]({{site.baseurl}}/img/2105_10_3.PNG)

> The more delay = longer we have to wait even thou the longer the delay = the less chance of delay


## Client side buffering, playout

![2105_10_4.PNG]({{site.baseurl}}/img/2105_10_4.PNG)



# Voice over IP
# rotocols for real time converational application
# Dynamic Adaptive streaming over HTTPS (DASH)
