How to Configure a VMWare Virtual Machine for OpenBSD Firewall
====================================================================================

Initial Steps
-------------
Sign in to VMWare server and login with a user that have appropriate permissions to perform the tasks of this document.

<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/vm1.png" width="70%" height="70%">


**Permissions:**

:white_check_mark: Create port groups

:white_check_mark: Upload ISO images

:white_check_mark: Create new virtual machines


Port Groups Configuration
--------------------------
In the left corner of the page click in 'Networking', right after you will see a buttom in the top center of the page named 'Add Port Group', click on it.

Each Port Group will be simulating a physical interface inside the virtual machine and will have a single VLAN ID (Example: 14, 15, 40, 100, 101 and 200).

:exclamation: If you are using a firewall cluster make sure the interface order are the same in both virtual machines. 

In the Advanced Security Options modify the following options:
```
Promiscuos Mode = accept 
MAC Address Changes = accept
Forged Transmits = accept
```

<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/vm2.png" width="70%" height="70%">

Note that port group was created:

<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/vm3.png" width="70%" height="70%">
  

Upload OpenBSD Image to Datastore
---------------------------------
We need to upload an image that would be used to install OpenBSD on this virtual machine.

In left corner click in 'DataStore', right after you will see on top center page a buttom named 'DataStore WebBrowser', click on it and in the next screen select upload and the image of distribution.
  
<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/iso1.png" width="70%" height="70%">
  
<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/iso2.png" width="70%" height="70%">
  
<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/iso3.png" width="70%" height="70%">

Virtual Machine
----------------
Now that the port group was created we will create a virtual machine, add all port groups to them, and start to install OpenBSD.

In the left corner click em Virtual Machines, right after you will see a buttom on top center page named 'Create/Register VM':
  
<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/vmg1.png" width="70%" height="70%">
  
Click in Next button, and set the name of virtual machine and the version compatibility of Vmware and distribution : 

```
virtual machine = name_of_your_virtual_machine
compatibility = ESXi 6.5 virtual machine
guest os family = Other
guest os version = Other 64bit
```

<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/vmg2.png" width="70%" height="70%">

In this step we will select a datastore to be used by the virtual machine

<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/vmg6.png" width="70%" height="70%">

<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/vm3.png" width="70%" height="70%">

In this step you are going to set up the hardware configuration for your virtual machine:

```
cpu = 2
memory = 2G
disk = 30GB
```
<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/vmg4.png" width="70%" height="70%">

In the Disk advanced options set:
```
Disk provisioning = Thick Provisioned, eagerly zeroed**
```
In the Network Adapter advanced options set:
```
vmxnet3
```

**LSI Logical SAS**

**Disk Drive = DatasStore Iso File / Instal62.iso**

<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/vmg5.png" width="70%" height="70%">


After defined basic hardware settings, let's go to create the virtual machine and click in Finish button:

<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/vmg7.png" width="70%" height="70%">

In this last step, start your virtual machine :

<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/vmg8.png" width="70%" height="70%">

