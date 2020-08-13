# Mobile IP

The TCP/IP protocol stock was built when computers were giant machine which had little or
no chance of ever moving around cut to the 21'st century computers are in everyones hands and
are constantly connecting and disconnecting to IP networks.

## The problem with mobile hosts in TCP/IP

* as seen in IP addressing the address is split into host and network, this hierarchical is integral to routing datagrams.
* IP address has high coupling with the network where the device is attached. 

The tight coupling implies that for a mobile host there are only two possible ways within
conventional IP to adjust IP with the mobile host changing its access point.

* Change the IP address 		: we can change the IP address of the host to a new address, including the new network id.
* Decouple IP routing from address	: we can change routing based on the network id to only on its IP address.
* Both these solutions are not practical, changing IP each time would require lots of overhead to notify its peers.
* Routing based on entire address will result in explosion of routing tables and wasting the careful structure of IP addresses.

## The solution mobile IP

A new protocol to support mobile devices called IP mobility support for IPv4 RFC 2002/3220
The goals of mobile IP are as follows :-
* seamless mobility using existing address
* No new addressing or routing requirements
* interoperability - needs to work with devices that are not mobile ip aware
* layer transparency - the changes made must not be felt by the upper layers and should be in network layer only.
* limited hardware changes - changed should be required only by the software of the device as well as routers directly used by the device
* scalability - the scope of connection change should be global and support any number of devices.
* security - the mobile IP works by redirecting messages so auth procedures should be provided to prevent unauthorized devices

Mobile IP uses a forwarding system for devices. When a unit is on its home network, it functions normally. 
When it moves to a different network datagrams are sent from its home network to its new location. This puts the
onus of rerouting completely on the device and its immediate peer routers.

## Limitations of mobile ip

* it is designed to  handle only to handle infrequent changes.
* it is also meant for devices that have static IP configuration

## The process

### The players

There are mainly three main players in the process
* Mobile node 	- this is the mobile device moving around in the network
* home agent  	- router in the home network responsible for catching datagrams intended for mobile node and forwarding them to where they are now.
* foreign agent - this the router in the network the mobile device is currently attached to 

### The functions

* Agent communication	-	finds and agent on its local network  by the agent discovery process that usually consists of listening for agent broadcast messages, but may use agent solicitation messages as well.
* Network location determination - the mobile node finds whether its on a home network or foreign one using the details from agent messages.
* If on home network it functions like normal IP.
* Care-off address acquisition - If the device is on a foreign network it will find out from the network location determination process. It acquires a temporary address called care-of address from the foreign agent, this is used as the destination point for forwarding datagrams
* Agent registration - the mobile node informs the home agent on its home network that is currently resides in a foreign network and enables data forwarding by registering its care-of address with the home agent
*  Datagram forwarding - now that all the registration is done and all the players know the location and address few the mobile device we can send the data to the new co address.
