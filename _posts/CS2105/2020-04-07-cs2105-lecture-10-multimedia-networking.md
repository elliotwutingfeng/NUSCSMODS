---
layout: post
published: true
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

1. Initial fill buffer until playout begins at tp
2. Playout begins at tp
3. Buffer fill level varies over time as fill rate x(t) varies and playout rate r is constant

![2105_10_5.PNG]({{site.baseurl}}/img/2105_10_5.PNG)

> If the data is coming as a slower rate, the buffer will drain faster and freeze the video

## Streaming multimedia: UDP
- Server sends at rate appropriate for client
   - OFten: Send rate = encoding rate = constant rate - > Push based streaming (Server push)
   - Transmission rate can be oblivious to congestion levels
   
- Short playout delay to remove network jitter
- Error recovery: Application level, time permitting
- RTP [RFC 2326]: Multimedia payload types
- UDP may not go through firewalls

## Streaming multimedia:HTTP
- Multimedia file retrieved via HTTP GET
  -> Pull base streaming (client pull)
- Send at max possible rate under TCP

![2105_10_6.PNG]({{site.baseurl}}/img/2105_10_6.PNG)

- Fill rate fluctuates due to TCP congestion control, retransmission
- Larger playout delay: Smooth TCP Delivery rate
- HTTP/TCP passes more easily through firewalls

# Voice over IP

- Need to maintain conversation aspect
   - small delay
   - Include application level network delays
- Session init: How does callee advertise IP address, port number, encoding algorithms
- Value-added services: Call forwarding, screening, recording
- Emergency services: 911

## Characterstics
- Speaker audio: Alternating talk spurts, silent periods
   - 64kbps talk spurt
   - Packet only generated during talk spurt
   - 20msec chunk at 8Kbytes/sec:160 bytes of data per chunk
- Application-layer header added to each chunk
- Chunk +header encapsulated into UDP or TCP
- Application sends segment into socket every few msec

## Packet loss, delay

- Network loss; IP datagram lost due to network congestion (router buffer overflow)
- Delay loss: IP datagram arrives too late for playout at receiver
   - delays: Processing, queuing, end sys delays
   - Typical tolerable delay: 400ms
- Loss tolenrance: Depending on voice encoding, loss concealment, packetloss rates between 1 to 10 percent can tolerate

> Our brain has an error recovery system such that even if there is a little dropout noise in a call, our brain can recover some of the missing parts

## Delay Jitter

Similiar to the graph before, the variable network delay is a jitter.

So we introduce a client playout delay.

## Fixed playout delay
- Reciever attempts to playout each chunk exactly q msec after chunk was generated
   - Chunk has time stamp t: playout chunk at t+q
   - Chunk arrives after t+q: data arrives too late for playout: date "lost"
- Tradeoff in choosing q:
   - Large q: less packet loss
   - Small q: better interactive experience

![2105_10_7.PNG]({{site.baseurl}}/img/2105_10_7.PNG)

## Adaptive playout delay

Goal: Low playout delay, low late loss rate

Approach: Adaptive playout delay adjustment
- Estimate network delay
- Adjust at beginning of each talk spurt
- Silent periods compressed and elogated
- Chunks still playout every 20 msec

![2105_10_9.PNG]({{site.baseurl}}/img/2105_10_9.PNG)

> Alpha is like a nob we can turn to see if we can use more of history or more of recent


![2105_10_8.PNG]({{site.baseurl}}/img/2105_10_8.PNG)

di is the middle of the bellcurve

> The first talk spurt has a longer delay compared to talkspurt.

![2105_10_10.PNG]({{site.baseurl}}/img/2105_10_10.PNG)


**Q: How does reciever determine whether packet is first in a talkspirt?**

> If no loss, receiver looks at successive time stamps

## Recovery from packet loss

When data is loss completely.
We can
1. Let it go
2. Do recovery via retransmission through application level
3. FEC (Forward Error correction)
   - Send enough bits to allow recovery without needing new transmission
   
### Piggyback

![2105_10_11.PNG]({{site.baseurl}}/img/2105_10_11.PNG)

> The low quality part of the previous is attached to the next packet.

THis means that they can retrieve the lower quality packet if its loss

### Error concealment

Packet interleaving

![2105_10_12.PNG]({{site.baseurl}}/img/2105_10_12.PNG)


- No redundancy
- Reorder the packet sequence and interleave the stream

This means that if the packet is loss, not every piece is missing.


# Protocols for real time converational application

## RTP (Real time protocol)
- Specifies packet structures for packets carrying audio, video data
- Carries an additional header that is media specific
- Time stamp
- Sequence number

Wholeidea: If two application has RTP means that they are compatible, but this is not the case in real life.

![2105_10_13.PNG]({{site.baseurl}}/img/2105_10_13.PNG)

> Sometimes people talk about RTP as 3 types of protocol

RTP: Media data (UDP)

RTCP: Use for signalling (UDP)

RTSP: Carries the commands (TCP)

> We do not want to loose data regarding comands

RTP Header:
- Sequence number
- Time stamps
- source ID

![2105_10_14.PNG]({{site.baseurl}}/img/2105_10_14.PNG)

![2105_10_15.PNG]({{site.baseurl}}/img/2105_10_15.PNG)

> The reciever needs to know if the data is compress or not

## RTP and QoS
- Rtp does **not** provide any thing to ensure it is real time or QoS gurantees
- RTP encapsulation only sen at end system (Not at intermediate routers)
- Its a transport layer protocol

#### WebRTC

> RTP use to be use for VOD, now companies are using different types of RTP.

RTP has been integrated into browser and it allows it to build RTC capabilities via simple JavaScript APIs.

## SIP: Session initiation protocol

Whole idea: Come up with a system that works much more internationally for VoIP over the internet.

- Country code
- Phone number

> Can use email address as a phone number no matter where the callee roams no matter what IP device the callee is using

# Dynamic Adaptive streaming over HTTPS (DASH)

Notes on streaming:

- RTP/RTSP/RTCP streaming has challenges
  - Not compatible
  - Need complex servers (Scheduling at server side)
  - Protocol use TCP and UDP (firewalls)
  - Difficult to cache data (There is no web caching)
- Advantages
   - Short to end latency
   
VoD:
- Can be wasteful if use HTTP streaming just GETs a whole vide when it might not be viewed fully

> Now the world has move to DASH

Main Idea of DASH:
- Use HTTP protocol to stream media
- Divide media into small chunks (Streamlets)


Adv: 
- Server is simple
- No firewall problems
- Standard image web caching works

Disadvantages
- Media segments are longer compared to RTP
- Latency can be quite low due to buffering (does not work for video conferencing)

## Works
- Take a whole video
- Cut into small pieces (Streamlets)
- Encode it into different quality files (Transcoded)

![2105_10_16.PNG]({{site.baseurl}}/img/2105_10_16.PNG)


MFD: Descibes whhat is available and what quality

- Webserver provides a playlist


Client run a ABR (Adaptive bitrate algorithm) which determins which segment do download

ie. If the bandwidth is low, it will pull the lower quality.

Streamlets are stitch back together at the client side. 

> Dash has replace VoD streaming protocols

Recently focus is on low latency due to live video streaming.
