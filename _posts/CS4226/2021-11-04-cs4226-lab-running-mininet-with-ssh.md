---
layout: post
published: true
title: 'CS4226 - Lab: Running Mininet with SSH only'
---
# Setup Infomation

This setup is only for those who does not want to use ubuntu vm and just purely want to run using the mininet ssh. In order for this setup to work, you need to be able to run mininet using ssh.
The software used is PUTTY and Winscp for windows users



##  Network Host Adapter Setup
In order to be able to ssh from your pc, you need to have this setup.
(If you already have this, you can skip this step)

1. From your Oracle Virtual Box, Click on File > Host Network Manager
	![CS4226_labsetup_1.png]({{site.baseurl}}/img/CS4226_labsetup_1.png)


2. Click on create and follow the following settings
	- Adapter:
    	- Check Configure Adapter Manually
        - IPV4 Address: `192.168.56.1`
        - IPV4 Network Mask: `255.255.255.0`
    - DHCP Server:
    	- Check Enable Server
    	- Server Address: `192.168.56.100`
        - Server Mask: `255.255.255.0`
        - Lower Address Bound: `192.168.56.101`
        - Upper Address Bound: `192.168.56.254`
  
  ![CS4226_labsetup_2.png]({{site.baseurl}}/img/CS4226_labsetup_2.png)




3. Ensure that it is enable
  ![CS4226_labsetup_3.png]({{site.baseurl}}/img/CS4226_labsetup_3.png)
  

## Mininet Network Setup
Ensure that the mininet and ubuntu both are connected using the network host adapter that was created the previous. **Note that the VM must not be running when creating this setting.**

Right click the VM > Setting > Network > Adapter 2 
- Enable Network Adapter
- Attached to: Host-only Adapter
- Name: **The name of the Network host adapter created**

![CS4226_labsetup_4.png]({{site.baseurl}}/img/CS4226_labsetup_4.png)

Theres no need to do any advance configuration

# SSH into Putty
In order to ssh into mininet using your setup, you need to know what the ip addess is for

## Mininet
Login Credentials: 
		- Login: mininet
        - Password: mininet


1. Check your configuration by running `ifconfig -a`
	![CS4226_labsetup_5.png]({{site.baseurl}}/img/CS4226_labsetup_5.png)



2. Setup Virtual box Additional Setup
	- Create dhclient
	```bash
	sudo dhclient eth1
	```
    - Edit the /etc/network/interfaces file using nano
	```shell
	sudo nano /etc/network/interfaces
    ```
    
    - Add the following lines below the code
    ```
    auto eth1
 	iface eth1 inet dhcp
    ```
    
    ![CS4226_labsetup_6.png]({{site.baseurl}}/img/CS4226_labsetup_6.png)

3. SSH into mininet using putty
	ip: (Check your `ifconfig`) `192.168.125.104`
    port: 22
    ![image_2021-10-20_232029.png]({{site.baseurl}}/img/image_2021-10-20_232029.png)

# Running Controller and Mininet using PUTTY

Open two putty console and run mininet on one console and the controller on the other. You can put your own controller into the Mininet setup using winscp file transfer protocol.

The following is some helpful commands for both

Running POX controller (forwarding learning):
- Example: `./pox.py log.level --DEBUG forwarding.l2_learning`
- My code: `./pox.py log.level --DEBUG misc.controller`

Running Mininet:
- Example: `sudo mn`
- My Code: `sudo python mininetTopo.py topology.in 0.0.0.0`

The following shows the sample setup:

Take note of the connectivity from the mininet topo to the controller:
![image_2021-11-04_173559.png]({{site.baseurl}}/img/image_2021-11-04_173559.png)


Explaination: Because our controller is hosted at localhost by default, the ip address our given to our topo is our localhost which has the ip address of `0.0.0.0`



