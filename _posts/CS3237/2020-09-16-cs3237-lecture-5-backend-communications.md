---
layout: post
published: false
title: 'CS3237 - Lecture 5: Backend Communications'
---
# Hypertext transfer protocl

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

## MIME Types
- Multipurpose internet Mail extension (MIME) types:
	- Extensible. Can define new MIME types
    - Common MIME types:
    	- Application/pdf
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
    