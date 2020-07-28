# IP datagram delivery and routing

The job of the IP protocol is to transmit messages from higher layer protocols, over an 
internetwork of devices. These messages must be packaged and addressed and if necessary 
fragmented, but the main part is delivery to the to the destination this process varies
based on the proximity of the source.

## Delivery types

* __direct delivery__ - when the datagrams are sent between two devices on the same physical network, the datagrams can be delivered directly without any 
* __indirect delivery__ - when two devices are not on the same physical network the delivery of datagrams from the source to destination is indirect. Since the destination isn't visible
to the source it will need to go through one or more intermediate routers to deliver it.

## Indirect delivery

As we can see direct delivery more or less operates entirely within the Link layer and does
not require IP routing and addressing, the Link layer simply tries to find the ARP table
* The source device and it's implementation tries to find an ARP entry for given IP.
* If found the dest is on the same network, and so it is framed with corresponding MAC address
* If not found the datagram is sent to the default gateway or the router that is configured to handle that type of address. 
* The router finds the next hop address and the datagram is routed using the IP routing protocols until it reaches the destinations local network.
* for routers that are connected to more than 2 devices will have to decide which path is most efficient for reaching a given destination.

## Classless networks routing 

The classless addressing scheme is called CIDR or classless inter-domain routing, the name
does not use addressing but routing to stress that it is designed to make routing more
efficient. CIDR is more efficient since it introduces a multiple level hierarchy hence a 
large number of IP devices may have the same route entry for many routers, its only when they
reach a certain proximity to the destinations location that we need more entries. This 
reduces the loads on routing tables greatly.



