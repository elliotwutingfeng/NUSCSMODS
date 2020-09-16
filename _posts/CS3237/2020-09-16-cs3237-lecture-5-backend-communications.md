---
layout: post
published: false
title: 'CS3237 - Lecture 5: Backend Communications'
---
# Hypertext transfer protocl
![CS3237-5-1.PNG]({{site.baseurl}}/img/CS3237-5-1.PNG)
![CS3237-5-2.PNG]({{site.baseurl}}/img/CS3237-5-2.PNG)

Phase:
- Connection: Open connection to the server
- Request: Make a request (GET, POST, PUT, DELETE)
- Response: Receive a response from the server
- Close connection: Close the connection to the server

HTTP Is stateless
- HTTP does not keep track of what happened in prev connections
- APplications backend must do this on its own through use of databases
- Application can deposit cookies in the browser to maintain states


## Request types
- GET: Request for a specific document (Can also be used to send data)
- POST: Request for server to accept data from browser
- PUT: Replace a document with data provided by browser
- DELETE: Remove a document
- HEAD: Retrive only header of document

Documents are in the form of HTML files:
- Consists of
	- Text that can be marked up to format
    - Hyperlinks: Links to other documetns possibly on other servers
    - Scripts: Programs that will be run on your browser

## MIME Types
- Multipurpose internet Mail extension (MIME) types:
	- Extensible. Can define new MIME types
    - Common MIME types:
    	- application/pdf
        - application/json
        - image/gif
        - image/jpg
- When request for a document using GET or POST, we shld specify the expected document type in the header.
E.g Content-Type: application/json

#### Creating a HTTP server in python
- Flask

# Message queuing telemetry transport

- ISO standard
- Advantages over HTTP:
	- Lightweight, less overheads
    - Public subscribe model
    	- Centralised server
        - Clients subscribe to topics
        - When someone publishes messages in a topic, all interested client are notified
- Contrast with HTML
	- Essentially a point to point (client to server) model
    - Client needs to continually poll the server using a client-side script to get updates.
    - Some imporvements are available to sovle this (Webscokets)

## Implementing
- Use Mosquitto
- `sudo apt-get install mosquitto mosquitto-clients`
- `pip3 install paho-mqtt`
- `sudo service mosquitto start`

## Programming
- Declare two listeners
	- on_connect: Called when the client has attempted to connect to a broker. Must get a result code of 0 for success
    - on_message: Called when the client has recieved a message on the topic it is subscribing to.
- Example Code: GIven in the slides

![CS3237-5-3.PNG]({{site.baseurl}}/img/CS3237-5-3.PNG)



##### See slides on how to use mosquitto

# Databases
