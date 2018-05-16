Step by Step to send Pflow Data from OpenBSD to Fluentd Agent -> Elastic Search
==============================================================================

In this tutorial we will see how to configure the OpenBSD to send pflow data to fluentd agent installed on a ElasticSearch Server.


Configuring Fluentd to receive Pflow Data
------------------------------

In the first step to receveive pflow data over Netflow plugin of ElasticSearch is build the Netflow Plugin in Fluentd, use this command :

```
/opt/td-agent/embedded/bin/fluent-gem install fluent-plugin-netflow
```

After the successful build of Netflow Plugin, edit the configuration file of Fluentd (/etc/td-agent/td-agent.conf) with the source and match config to respectively receive the pflow data and send to ElasticSearch index :

source config :
```
<source>
  @type netflow
  port 2205
  bind 0.0.0.0
  tag netflow
</source>
```

match config :
```
<match netflow>
  @type elasticsearch
  logstash_format true
  host 127.0.0.1
  port 9200
  index_name fluentd
  type_name fluentd
</match>

```

:exclamation: Restart the Fluentd service after changes

```
/etc/init.d/td-agent restart
```

Now the FLuentd Agent is ready to receive Pflow data and send to ElasticSearch server.

Configuring the OpenBSD to send pflow data to Fluentd Agent
-----------------------

Initially identify with a simple ping command what interface can talk with the Fluentd Agent / ElasticSearch :

```
ping <ip_of_fluentd_agent>
```

After identify the interface, see the IP address from it :

```
ifconfig <interface>
```

Now whit the interface name and ip address, we will configure the pflow interface to send data to Fluentd Agent / ElasticSearch with this command :

```
ifconfig pflow0 flowsrc <ip_of_interface> flowdst <ip_of_fluentd_agent>:2205
```

And finalizing the pflow interface, set the version of pflow protocol supported in your agent, in this case we're using td-agent 0.12 that support pflow protocol leve 5,6 and we use the version 5 :

```
ifconfig pflow0 pflowproto 10
```

To view the result of your configurations apply this command :

```
ifconfig pflow0
```

<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/pflow0.png" width="70%" height="70%">

Testing the functionality of communication
-----------------------

To test if the configuration is OK, you can view the pflow data comming on fluentd agent with a simple tcpdump :

```
tcpdump -i <interface> src <ip_of_openbsd> and dst <ip_of_fluentd_agent> and port 2205
```

<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/tcpdump1.png" width="70%" height="70%">

You should view UDP packets comming naturally to your fluentd agent, now just check in your ElasticSearch if the data is comming to index configured on your match config (/etc/td-agent/td-agent.conf), in this case we use the Kibana as FrontEnd Dashboard to ElasticSearch and Discover tab we see the traffic comming from our OpenBSD :

<img src="https://github.com/alexfrosa/openbsd-pf-formula/raw/master/images/kibana1.png" width="70%" height="70%">
