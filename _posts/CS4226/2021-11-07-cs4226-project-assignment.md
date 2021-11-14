---
layout: post
published: true
title: CS4226 - Project Assignment
subtitle: Project Assignment
---

# Github
Github Repository: [Link](https://github.com/Deunitato/CS4226_Project)




# Task 1 - Setting up the topology

Setting up the topology using the topology.in file. The only file you need to enter is 


```python
# Add switch
 for x in range(1, int(switch) + 1):
      sconfig = {'dpid': "%016x" % x}
      self.addSwitch('s%d' % x, **sconfig)
 # Add hosts
 for y in range(1, int(host) + 1):
      self.addHost('h%d' % y)

 # Add Links
 for x in range(int(link)):
      info = linksInfo[x].split(',')
      host = info[0]
      switch = info[1]
      bandwidth = int(info[2])
      self.addLink(host, switch, bw=bandwidth)
```

# Task 2 - Learning switch

# Task 3 - TTL 
We should just set a TTL of 30 for each new entry flow as well as clear the table in our controller everytime a change is detected.

The following output from the controller will be shown every time a link is dropped:
![image_2021-11-14_191854.png]({{site.baseurl}}/img/image_2021-11-14_191854.png)

Output:

![CS4226_task3_2.png]({{site.baseurl}}/img/CS4226_task3_2.png)



# Task 4 - Firewall
Debug:
Running the command `sh ovs-ofctl dump-flows s1` would let us see the current flow table.
You can check if firewall is corrrectly set if it shows the `action=any` as the flow entry as shown in the following image
![CS4226_task4_2.png]({{site.baseurl}}/img/CS4226_task4_2.png)


Output:

![CS4226_task4_1.png]({{site.baseurl}}/img/CS4226_task4_1.png)


# Task 5
In order to understand what we are trying to do, we need to understand the code in question. The professor has already kindly gave us the needed code for us to our work

```python
# Create QoS Queues
os.system('sudo ovs-vsctl -- set Port [INTERFACE] qos=@newqos \
     -- --id=@newqos create QoS type=linux-htb other-config:max-rate=[LINK SPEED] queues=0=@q0,1=@q1,2=@q2 \
     -- --id=@q0 create queue other-config:max-rate=[LINK SPEED] other-config:min-rate=[LINK SPEED] \
     -- --id=@q1 create queue other-config:min-rate=[X] \
     -- --id=@q2 create queue other-config:max-rate=[Y]')
```

What this code is doing is we are creating **3** queues with the id `0`, `1`, `2`. In this case, we are trying to create 3 queues with the following specs:
- [q0] (Basic queue): Max and Min of 1000000
- [q1] (Premium queue): min rate of 0.8 x 1000000
- [q2] (Free queue): Max rate of 0.5 x 1000000

We would set each link to each switch port to have the choice of any of these 3 queues. The queues will be selected by our controller later.

## Getting all the links
The following code chunk would print out all the links available 

```python
    for link in topo.links(sort=True,withKeys=False, withInfo=True):
    	print(link)
```
Printing out all the links setup:
![image_2021-11-10_001816.png]({{site.baseurl}}/img/image_2021-11-10_001816.png)


## Assigning the queue
Queues can only be configured at switch ports. This is indicated by the black dots shown in the following image: 
![CS4226_task5_2.png]({{site.baseurl}}/img/CS4226_task5_2.png)

We can assign the queue using the the links and bandwidth. The following shows the ports

Printing the ports:
![CS4226_task5_5.png]({{site.baseurl}}/img/CS4226_task5_5.png)
![CS4226_task5_6.png]({{site.baseurl}}/img/CS4226_task5_6.png)


Ports connected for each switch:
![CS4226_task5_3.png]({{site.baseurl}}/img/CS4226_task5_3.png)


## Results
![CS4226_task5_4.png]({{site.baseurl}}/img/CS4226_task5_4.png)


References:
[[OpenFlow Docs](https://openflow.stanford.edu/display/ONL/POX+Wiki.html#POXWiki-Enqueue)], [[Some Slide from another school](http://csie.nqu.edu.tw/smallko/sdn/mySDN_Lab5.pdf)], [[POX controller documentation](https://openflow.stanford.edu/display/ONL/POX+Wiki.html#POXWiki-SetTCP%2FUDPsourceordestinationport)]
