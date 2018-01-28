vagrant-ksql
=============
### A vagrant provided kafka cluster with ksql servers for tests usage

This vagrant boot a three node kafka cluster, available on port 9092 outside the vagrant.
The new ksql feature from Confluent (currently in beta) is also installed on each nodes.

Installation
------------

``` bash
# from the cloned project
vagrant up

```

You can set any node you want from the Vagrantfile.

ksql
------------

ksql servers are already started and can be accessed from anywhere outside the vagrant at the folling locations:
``` bash
http://192.168.33.33
http://192.168.33.34
http://192.168.33.35
```


If you are using the Confluent ksql-cli (the only one available for now)

``` bash
# from vagrant ksql folder 
/opt/ksql/bin/ksql-cli remote http://192.168.33.33:8080
```