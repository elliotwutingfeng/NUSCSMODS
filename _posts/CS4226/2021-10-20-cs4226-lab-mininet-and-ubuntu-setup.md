---
layout: post
published: true
title: 'CS4226 - Lab: Mininet and Ubuntu Setup with Virtual Box'
subtitle: A indept Guide on Setting up Mininet and ubuntu vm with Virtual Box
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
    - Ping h1 to h2
    ```bash
    mininet> h1 ping h2
    ```
    - Ping all
    ```bash
    mininet> pingall
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

1. Clone pox and use the correct version
	```bash
    git clone https://github.com/noxrepo/pox
    cd pox
    git checkout fangtooth
    ```

2. Start Pox
	```bash
    ./pox.py log.level --DEBUG forwarding.l2_learning
    ```
    You should see the following sample output:
    ![image_2021-10-20_232758.png]({{site.baseurl}}/img/image_2021-10-20_232758.png)
    
    This means that pox controller is located at 0.0.0.0 for our Ubuntu but accessing it from outside would use `<Ubuntu_IP>` which in this case is `192.168.125.103`

3. Start mininet
    Since Ubuntu is running at `192.168.125.103`, we would use it to connect our mininet vm with.
   	
    ```bash
    sudo mn --controller=remote,ip=192.168.125.103,port=6633
    ```
    > Ensure that theres no space between the commas

4. Check your ubuntu
	You should be able to see a new connection from your ubuntu pox controller. This means you have successfully connected both your mininet and your pox controller!


Sample Ubuntu output pox:
![CS4226_labsetup_10.png]({{site.baseurl}}/img/CS4226_labsetup_10.png)

Sample Mininet output:

![image_2021-10-20_233440.png]({{site.baseurl}}/img/image_2021-10-20_233440.png)

Note: 2 commands were used, `pingall` and `h1 ping h2`



## References
- [Mininet Virtual Box Extra Setup](https://github.com/mininet/openflow-tutorial/wiki/VirtualBox-specific-Instructions)
