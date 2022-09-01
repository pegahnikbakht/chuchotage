# Chuchotage 
In-line protocol translator for (D)TLS

To run the test and examples you need to install Open vSwtich (OVS) on the host machine, follow the steps on https://github.com/openvswitch/ovs/blob/master/Documentation/intro/install/general.rst to install and configure. 

After installing OVS create a bridge using: 
```sudo ovs-vsctl add-br br0```

Configure internal IP address for your bridge: 

```sudo ifconfig br0 173.16.1.1 netmask 255.255.255.0 up```

Create four different docker containers that are going to represnt your SDN controller, client, server, and Intel SGX (using Occlum). 
