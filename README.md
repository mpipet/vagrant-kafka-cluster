vagrant-kafka-cluster
=============
### A kafka cluster vagrant for dev usage

This vagrant boot a three node kafka cluster, available on port 9092 outside the vagrant.


Installation
------------

``` bash
# from the cloned project
vagrant up

```

ksql
------------
The new ksql feature from Confluent (currently in beta) is also installed

ksql server is already started and can be also accessed from anywhere outside the vagrant with:

``` bash
# from vagrant ksql folder 
/opt/ksql/bin/ksql-cli remote http://192.168.33.33:8080
```
You can also acess the ksql server on the two oser nodes:
http://192.168.33.34 and http://192.168.33.35