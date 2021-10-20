---
layout: post
published: false
title: 'CS4226 - Lab: Mininet and Ubuntu Setup'
---
# Setup Notes given

Note: Click on the view button to see the full size.

# In-depth Setup configuration

Setup overview:
- 2 VM
	- [Ubuntu 18](https://releases.ubuntu.com/18.04.6/ubuntu-18.04.6-desktop-amd64.iso)
    - [Mininet 2.2.2](https://github.com/mininet/mininet/releases/download/2.2.2/mininet-2.2.2-170321-ubuntu-14.04.4-server-amd64.zip)
    - Putty (Optional)
    
## VM Setup

#### Network Host Adapter Setup

(If you already have this, you can skip this step)

1. From your Oracle Virtual Box, Click on File > Host Network Manager
	![CS4226_labsetup_1.png]({{site.baseurl}}/img/CS4226_labsetup_1.png)

2. Click on create and follow the following settings
	Adapter:
    	- Check Configure Adapter Manually
        - IPV4 Address: `192.168.56.1`
        - IPV4 Network Mask: `255.255.255.0`
    DHCP Server:
    	- Check Enable Server
    	- Server Address: `192.168.56.100`
        - Server Mask: `255.255.255.0`
        - Lower Address Bound: `192.168.56.101`
        - Upper Address Bound: `192.168.56.254`
  
  ![CS4226_labsetup_2.png]({{site.baseurl}}/img/CS4226_labsetup_2.png)

3. Ensure that it is enable
![CS4226_labsetup_3.png]({{site.baseurl}}/img/CS4226_labsetup_3.png)

#### Ubuntu and Mininet Network Setup
Ensure that the mininet and ubuntu both are connected using the network host adapter that was created the previous. **Note that the VM must not be running when creating this setting.**

Right click the VM > Setting > Network > Adapter 2 
- Enable Network Adapter
- Attached to: Host-only Adapter
- Name: **The name of the Network host adapter created**

![CS4226_labsetup_4.png]({{site.baseurl}}/img/CS4226_labsetup_4.png)

Theres no need to do any advance configuration














