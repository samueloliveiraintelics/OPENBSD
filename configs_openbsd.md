Configurations Post-Installation OpenBSD
==============================================================================

Identifying Network Interfaces
------------------------------

To identify network interfaces, enter the command bellow and see the result of command, what traffic is going on it :
```
tcpdump -n -e -vvv -i <interface>
```

<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/tcpdump.png" width="70%" height="70%">

:exclamation: In this case the traffic going on vmx5 is traffic of Vlan 14.

Network Configurations 
-----------------------

**Pf-Obj.conf**

Configure the name of groups that will be used on configuration files of network interfaces on /etc/pf-obj.conf

<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/pfobj.png" width="70%" height="70%">

**PfSync**

Configure the pfsync interface with the bellow config file /etc/hostname.pfsync0

<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/pfsync.png" width="70%" height="70%">

```
up syncdev vmx4
```
**Physycal Interfaces**

Configure the physical interfaces on /etc/hostname.vmxX

<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/hostname_vmx.png" width="70%" height="70%">

```
inet 10.28.14.5 255.255.255.0
group wifiguest
```

:exclamation: Atention in this step, configure the physical interfaces following the results obtained in the identification of interfaces whit tcpdump 

:exclamation: The group named in this config file must be the same of /etc/pf-obj.conf 

**Carp Interfaces**

Configure the Carp interfaces on /etc/hostname.carpX 

<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/hostname_carp.png" width="70%" height="70%">


```
inet 10.28.14.1 255.255.255.0 10.28.14.255 vhid 14 pass ximbica advbase 2 advskew 0 carpdev vmx5
```

**Physycal Interface of Traffic Vlan** 

In the physical interface of traffic vlan, we need set some different configurations, we will set too in this file the static routes to others vlans that firewall corp not manage 

<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/physycal_200.png" width="70%" height="70%">

```        
inet 10.28.200.5 255.255.255.0
group transito
!route add -net 10.28.1/24 10.28.200.4
!route add -net 10.28.5/24 10.28.200.4
!route add -net 10.28.6/24 10.28.200.4
!route add -net 10.28.10/24 10.28.200.4
!route add -net 10.28.11/24 10.28.200.4
!route add -net 10.28.12/24 10.28.200.4
!route add -net 10.28.16/24 10.28.200.4
!route add -net 10.28.20/24 10.28.200.4
!route add -net 10.28.21/24 10.28.200.4
!route add -net 10.28.30/24 10.28.200.4
!route add -net 10.28.14/24 10.28.200.5
!route add -net 10.28.15/24 10.28.200.5
```

Enable IP Forwarding, Ip Multipath Route on /etc/sysctl.config, configure as bellow :

<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/sysctl.png" width="70%" height="70%">

```
net.inet.ip.forwarding=1
net.inet.ip.multipath=1
ddb.panic=0
```


Salt Minion
------------

To install salt minion and configure to comunicate with Salt Master Intelics, follow this steps

```
pkg_add salt_minion
```

<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/salt_install.png" width="70%" height="70%">

After, configure the salt minion file with bellow itens :

```
id: <hostname>.<domain.local>
master: master.intelics.com.br
```

<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/salt_config.png" width="70%" height="70%">

In the end of config, enable to start at statrup time and star the service :

```
rcctl enable salt_minion
rcctl start salt_minion
```

<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/salt_enable_start.png" width="70%" height="70%">
