## How to install a OpenBSD 6.2 Distribution clean to Firewall
#### This tutorial have as objective the basic installation of OpenBSD Distribution, when we start a configure PF Firewall

#### Step 1 
Boot the virtual machine from disk or bootable media with the OpenBSD 6.2 x64, and the firts screen enter "I" to Install :

![Install Screen](/images/pic1.png)

#### Step 2
Select the layout of your keyboard and set the hostname for the virtual machine :

**keyboard = br**

![Keyboard e Hostname Screen](/images/pic2.png)

#### Step 3 
=======
In this screen the instalation guide will show the available network interfaces to configure, enter em0 :

![Network Interfaces Screen](/images/pic3.png)

#### Step 4
=======
In this step DON'T configure anynoe interface as 'DHCP' enter 'none' and 'none' to finish configuration of network address :

![Network Address Screen](/images/pic4.png)

#### Step 5 
=======
Set the domain name of your machine to build the Fully Qualified Domain Name :

**domain name = sp.ad.escaleseo.com.br**

![Domain Name Screen](/images/pic5.png)


#### Step 6
=======
In this step set the IP Address of your DNS Server

**dns server = 10.28.30.16**

![DNS Server Screen](/images/pic6.png)

#### Step 7 
=======
Set the root password :

![Root Password Screen](/images/pic7.png)

#### Step 8
=======
Enable or Disable the SSH Service :

![Enable/Disable SSH Screen](/images/pic8.png)


#### Step 9
Choose "no" to install X server to enable graphical access, and remove the X paths to instalation

**set = no**

![X Server Screen](/images/xserver_1.png)

**Enter '-x and asterisk' to remove the graphical paths in instalation**

![X Server Screen 2](/images/xserver_2.png)

**The installation will be like this :**

![X Server Screen 3](/images/xserver_3.png)

Set the local user to create :

**user = intelics**

![Local User Screen](/images/pic10.png)


#### Step 11
=======
Enable or Disable Root login above SSH Connection :

**root login = 'no'**

![Enable/Disable Root Login Screen](/images/pic11.png)


#### Step 12 
=======
Choose the primary disk where the /boot will be installed and agree with the automatic configuration :

**In this wizzard enter 'W' and 'A' for select the type of partition and the automatic install**

![Choose Disk](/images/pic12.png)

#### Step 13
=======
Choose the instalation of assets from media of instalation and agree with the sugestion of pathname to Kernel :

![Assets source](/images/pic13.png)

#### Step 14 
=======
Agree with the instalation of assets of kernel 6.2 :

![Assets structure Screen](/images/pic14.png)

#### Step 15
=======
Enter 'yes' to accept the installation without hash verification :

![Hash no Screen](/images/pic15.png)


#### Step 16
=======
Set the timezone of your country/state :

**timezone = Brazil/East, first enter 'Brazil', before enter 'East'**

![Timezone Screen](/images/pic16.png)


#### Step 17
=======
End of installation of distribution

![Finish Screen](/images/pic17.png)
