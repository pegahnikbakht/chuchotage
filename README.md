# Chuchotage 
In-line protocol translator for (D)TLS

To run the test and examples you need to install Open vSwtich (OVS) on the host machine, follow the steps on https://github.com/openvswitch/ovs/blob/master/Documentation/intro/install/general.rst to install and configure. 

After installing OVS create a bridge using: 

```sudo ovs-vsctl add-br br0```

Configure internal IP address for your bridge: 

```sudo ifconfig br0 173.16.1.1 netmask 255.255.255.0 up```

Create four different docker containers that are going to represent your SDN controller, client, server, and Intel SGX (using Occlum). 
After creating the docker containers connect them to the OVS bridge using: 

```
sudo ovs-docker add-port br0 eth1 [SDNdocker] --ipaddress=173.16.1.2/24
sudo ovs-docker add-port br0 eth1 [clientdocker] --ipaddress=173.16.1.3/24
sudo ovs-docker add-port br0 eth1 [serverdocker] --ipaddress=173.16.1.4/24
sudo ovs-docker add-port br0 eth1 [occlumdocker] --ipaddress=173.16.1.5/24
```
