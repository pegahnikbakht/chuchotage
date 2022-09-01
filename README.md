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
Set the SDNdocker as your OVS controller using the following command: 

```sudo ovs-vsctl set-controller br0 tcp:173.16.1.2:6633```

Connect to the docker containers using the follwoing command: 

```docker exec -it [containerID] bash```

Download and install Ryu on SDN docker from: https://github.com/faucetsdn/ryu
Place the trasnaltor.py inside the app/ directory and run the app using the following command: 

```ryu-manager translator.py```

Download FreeCoAP from https://github.com/keith-cullen/FreeCoAP and place it inside these three docker containers: clientdocker, serverdocker, occlumdocker. 

Download Occlum from https://github.com/occlum/occlum and place it inside occlumdocker as well. 
Complie the HTTP to CoAP parser with occlum-gcc, initilize an occlum instance and create an occlum SGX enclave (use simulation mode if your platform does not support SGX), using the occlum run you can now run the parser inside the occlum SGX enclave, for more details refer to https://github.com/occlum/occlum. 

Go inside serverdocker and make and run coap server example.
Later go inside clientdocker and make and run the http client example, make sure to change the IP addresses inside test_http_client.c before make. 

Now inside the clientdocker, you should see that your packets are successfully delivered to the CoAP server and you successfully get replies from the server. 



