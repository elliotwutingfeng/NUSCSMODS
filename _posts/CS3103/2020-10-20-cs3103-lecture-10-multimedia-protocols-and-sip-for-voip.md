---
layout: post
published: false
title: 'CS3103 - Lecture 10: Multimedia protocols and SIP for VOIP'
---
# Streaming audio/video
![CS3103-10-1.PNG]({{site.baseurl}}/img/CS3103-10-1.PNG)


## Streaming using a web server
![CS3103-10-2.PNG]({{site.baseurl}}/img/CS3103-10-2.PNG)

- Browser makes a request for file
- Response has the file
- File is send to the media player

## Streaming using webserver with metafile
![CS3103-10-3.PNG]({{site.baseurl}}/img/CS3103-10-3.PNG)

- Client request webserver
- Webserver sends more more details about the audio
- metafile is sent to the media player
- media player makes a seperate connection


## Streaming using a media server
![CS3103-10-4.PNG]({{site.baseurl}}/img/CS3103-10-4.PNG)

- Similiar
- Media server just focus on serving the media player


## Streaming using media server and rtsp
In the past: Can only stream data but cannot rewind forward etc etc.
- RTSP : Real time stream protocol, provides the different calls such as record, option, play pause
![CS3103-10-5.PNG]({{site.baseurl}}/img/CS3103-10-5.PNG)


## Streaming live vs Stored audio/video
- Stream live audio and video
-

# RTP
# RTCP
# RTSP
# SIP
# SDP
