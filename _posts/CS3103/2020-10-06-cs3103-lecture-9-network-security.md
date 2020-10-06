---
layout: post
published: false
title: 'CS3103 - Lecture 9: Network Security'
---
# Link state routing
Each router in the network knows the link state so that they can plan the appropriate path
- Distance vector: Router knows only cost to each destination
- Link state: Router knows the entire network topologu
	- Computes shortest path by itself
    - Independent computation of routes
    
![CS3103-8-1.PNG]({{site.baseurl}}/img/CS3103-8-1.PNG)

#### Forming shortest path tree for router A in a graph (Dik Algo)
![CS3103-8-2.PNG]({{site.baseurl}}/img/CS3103-8-2.PNG)
![CS3103-8-3.PNG]({{site.baseurl}}/img/CS3103-8-3.PNG)

THe cost can be anything depending on the protcol (like latency)

Reading the table:
![CS3103-8-4.PNG]({{site.baseurl}}/img/CS3103-8-4.PNG)
