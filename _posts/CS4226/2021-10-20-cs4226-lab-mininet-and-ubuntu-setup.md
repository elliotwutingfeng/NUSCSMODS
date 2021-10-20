---
layout: post
published: false
title: 'CS4226 - Lab: Mininet and Ubuntu Setup with Virtual Box'
---
# Setup Notes given

Note: Click on the view button to see the full size.

# In-depth Setup configuration

Setup overview:
- 2 VM
	- [Ubuntu 18](https://releases.ubuntu.com/18.04.6/ubuntu-18.04.6-desktop-amd64.iso)
    - [Mininet 2.2.2](https://github.com/mininet/mininet/releases/download/2.2.2/mininet-2.2.2-170321-ubuntu-14.04.4-server-amd64.zip)
    - Putty (Optional)
    - Virtual Box
    
## VM Setup

### Network Host Adapter Setup

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





### Ubuntu and Mininet Network Setup
Ensure that the mininet and ubuntu both are connected using the network host adapter that was created the previous. **Note that the VM must not be running when creating this setting.**

Right click the VM > Setting > Network > Adapter 2 
- Enable Network Adapter
- Attached to: Host-only Adapter
- Name: **The name of the Network host adapter created**

![CS4226_labsetup_4.png]({{site.baseurl}}/img/CS4226_labsetup_4.png)

Theres no need to do any advance configuration

## Mininet
Login Credentials: 
		Login: mininet
        Password: mininet


1. Check your configuration by running `ifconfig -a`
	![CS4226_labsetup_5.png]({{site.baseurl}}/img/CS4226_labsetup_5.png)



2. Setup Virtual box Additional Setup
	- Create dhclient
	```bash
	sudo dhclient eth1
	```
    - Edit the /etc/network/interfaces file using nano
	```bash
	sudo nano /etc/network/interfaces
	```
    
    - Add the following lines below the code
    ```
    auto eth1
 	iface eth1 inet dhcp
    ```
    
    ![CS4226_labsetup_6.png]({{site.baseurl}}/img/CS4226_labsetup_6.png)

3. (OPTIONAL) SSH into mininet using putty
	ip: (Check your `ifconfig`) `192.168.125.104`
    port: 22
    ![image_2021-10-20_232029.png]({{site.baseurl}}/img/image_2021-10-20_232029.png)

4. Test Mininet
	- Start Mininet
    ```bash
    $sudo mn
    ```
    - Check the nodes
    ```bash
    mininet> nodes
    ```
    - Check the network
    ```bash
    mininet> net
    ```
    - Check the nodes ifconfig
    ```bash
    mininet> h1 ifconfig
    ```
    - Quit MN
    ```bash
    mininet> quit
    ```
    - Clear settings
    ```bash
    $sudo mn -c
    ```


## Check Configuration on both VM
1. Run `ifconfig` on both VM
	
    - Mininet
    ![CS4226_labsetup_5.png]({{site.baseurl}}/img/CS4226_labsetup_5.png)
    - Ubuntu
    ![image_2021-10-20_231515.png]({{site.baseurl}}/img/image_2021-10-20_231515.png)

	From this, we can tell that Mininet is hosted at `192.168.125.104` and Ubuntu is located at `192.168.125.103`

2. Ping both side
	Run the following on both VM
    - On Ubuntu VM
    ```bash
    ping 192.168.125.104
    ```
    - On Mininet
    ```bash
    ping 192.168.125.103
    ```
> If its correctly configured, it should be pinged successfully


## POX

Pox only runs on python2 so ensure that your not executing python3 at all times. The following test would determine if and if 

1. Clone pox
	```bash
    git clone https://github.com/noxrepo/pox
    ```

2. Start Pox
	```bash
    git clone https://github.com/noxrepo/pox
    ```
    
    















