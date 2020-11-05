---
layout: post
published: false
title: 'CS2107 - Lecture 10: Web security'
---
# Background
Overview:
1. User click on url link
2. Http request is sent to server
3. Server construct and include a html file inside its HTTP response to the browser (Possibly with set cookie headers)
4. Browser renders the html files, which describe the layout to be rendered and presented to the user and any cookies are stored in the browser

## Sub-resource of a webpage
- COntain subresoources (Images, multimedia files, css, scripts) including from external party
- Browser will contact the respective server for the resources
- Seperate http request for every singe file on a page

## Request and Response format

## Web client and server components
- Client:
	- HTML: Webpage content
    - CCS: Webpage presentation
    - JS: Webpage behavior, making pages responsive and interactive
- Server:
	- Web server: Scripting language is typically use as well
    - Database server: Interaction between webserver and database server via sql
# Security issues and threat models