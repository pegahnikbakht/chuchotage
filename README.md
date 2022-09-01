# chuchotage 
In-line protocol translator for (D)TLS

To run the test and examples you need to install Open vSwtich (OVS) on the host machine, follow the steps on https://github.com/openvswitch/ovs/blob/master/Documentation/intro/install/general.rst to install and configure. 

After installing OVS create a bridge using: 
```
sudo ovs-vsctl add-br br0
```
