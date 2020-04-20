---
layout: post
published: true
title: CS2105 - Mock Examination questions
---
## Mock Examination Questions

<iframe src="https://drive.google.com/file/d/1UEoUgVSbITJcGS_wU-UA-cz6HA_YtF7c/preview" width="600" height="680"></iframe>

## Notes

Below are my opinions:

### q3

"hold an ACK" means not sending an ACK immediately.
Since it is an accumulative ACK, usually it is better to get a few more segments before sending out one ACK (which is able to ack all the segements received in order), instead of sending one ACK for one segement.

### q7

"Use more routers" does not imply using more private networks.
"Routers" are just to route packets.
You should treat "NAT" as an orthogonal/independent technology that can be enabled in a router.

### q9


a) Removing data from silence does not mean that the timestamps in the subsequence samples in the smae spurt will be modified. The client side still has to play the samples according to their relative sampled times.

b)

I think the diagram is just for illustration purpose. What (b) texts say is that if the network jitter is lower, you can move the playout point (p) closer to (not exactly at) the time the first pkt arrived (r). This sounds right to me.

### q8

from lecture notes 6:
Private addresses include:
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16


### q15

note that the sequence number in a TCP segment is the byte id of the first byte in the segment.
every payload is 100 bytes, so no matter what you should not get S=71.
![tcp_acks.png]({{site.baseurl}}/img/tcp_acks.png)

Also note that Y is also sending 100 bytes in each of its replies.

e.g. for the first packet from X, S=30, A=70; Then the first reply from Y should have: S=70 (Y's data starts from the 70th byte), A=130 (Y expects the next segment from X should have a seq number of 130)."

Then you just carefully label the S and A for the subsequent segments from X and Y respectively (from the perspectives of X and Y when they send segments)

![]({{site.baseurl}}/img/tcp_acks.png)