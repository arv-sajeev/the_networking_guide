# IP subnet addressing scheme

In the classful addressing scheme large organization are assigned a monolithic chunk of 
addresses this makes it really difficult to manage the address space. The subnet addressing
method adds another level of hierarchy. The network now consists of sub-networks which in turn consists of hosts.

## Advantages of subnet addressing

* more similar to the physical network structure
* flexibility to allocate within an organization 
* invisibility to the outside world
* reduces size of routing tables

## Implications

* The addressing scheme uses the classful technique to split the network and host-id, it also requires an additional 32 bit number called the subnet mask to split the sub-net and host-id
* The routers now need to take care of three scenarios, if the devices are on the same subnetwork,if they are on different subnets on the same network and if they are on a different network entirely

## The subnet masks

* the routers can use the first octet of the IP address to determine the class of the address this can be then used to find the split point of the network id and host id.
* we supply and additional 32 bit number which in binary form has ones where the subnets IP will be.
* by bitwise anding with the devices IP address we get the sub-networks IP
* each network has default subnet masks representing the network IP as in the classful address scheme, this mask would depend on class and is 8,16,24 for class A,B and C
* the number of subnets is 2^ the length of the subnet id, the hosts on the network are 2^host-id-length - subnet-id-length
* also take note that the all 0's host and all 1's host id have special meanings, this network and all hosts on the network.So the number of hosts of is decremented by 2. this also makes it stupid to have a subnet configuration that leaves just one host-id bit.

Just read a couple examples it's much harder to explain in words.

### IP variable length subnet masking (VLSM)

Single level subnetting only gives a one additional level and is not dynamic, once we decide
the mask size all the sub-networks size and sub-net-id all have the same size. In VLSM we 
are allowed to further subnet sub-networks  creating subnets of subnets.

## CIDR

As the internet grew and its addressing scheme evolved, problems kept rising, classful 
addressing made very inefficient use of the address space and had very low granularity.
Subnetting was used to solve some of these problems but the large disparity of hosts range
in the different classes was still a problem. Subnetting could only change the granularity 
within a class. The idea then was to eliminate classful addressing schemes and replace it
with CIDR

* efficient address space allocation
* elimination of class imbalances
* efficient routing entries
* uses a similar subnetting method
* much more complex to understand and process.
* it makes the address allocation more centralized and dynamic




