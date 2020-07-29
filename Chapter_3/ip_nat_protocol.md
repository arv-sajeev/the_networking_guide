# IP Network Address Translation Protocol

This is sort of a well-planned quick fix to solve the exhaustion of the IPv4 address space.
It allows a small number of public IP addresses to be used by a large number of hosts using 
private address.

## Indirect internet connectivity

One solution was to set up a system where the companies network wasn't connected directly to
the internet but indirectly.
* Most of the hosts on the network are clients and don't have to be publicly addressable all the time
* Only few hosts of a network access the internet simultaneously.
* The internet communications are routed

This is the concept behind NAT, it involves setting up an organization's internal network 
using one of the private addressing ranges set aside for local IP networks and the
organization is given one or more NAT capable routers.

### Advantages of NAT

* __public address sharing__ - A large number of hosts can share the same Public IP address
* __easier expansion__	     - since you don't need a new public IP address for each new client it is easier to add new hosts to a network.
* __greater local control__  - Get the benefits of a local network but still have access to the internet.
* __more flexibilty__	     - easier to change ISP
* __increased security__     - The NAT creates a sort of firewall between the organization and the public internet.


### Disadvantages

* It is complex
* Lack of real public address may pose problems in certain cases
* Tough to combine with IPsec since the address manipulation maybe seen as malicious
* Tough to access clients
* Performance reduction the extra processing can be seen as drawback

--- 

## IP NAT terminology

### NAT address terms based on device location

The first classification is based on where in the network the device referred to by the address is.
* Inside address - Any device that is on the organizations private network that uses NAT is said to be on the inside network and its addresses are called inside address
* Outside address - Any address that refers to a public internet device.

### NAT address terms based on datagram location

An inside device always has an inside address and outside device always has an outside 
address but there are two ways we can address them based on which part of the network the
datagram is 

* Local address - The address that appears in a datagram when it is in an inside network
* Global address - Describes an address that appears on the outside network.

## IP NAT static and dynamic address mappings

The NAT allows us to connect a private network to the public network using an address 
translation algorithm implemented in the router that acts as a gateway for both of them.
The software needs to maintain a mapping between the local addresses of internal devices and 
the inside devices global representation.

### Static mappings

A permanent fixed relationship is defined between the global and local representation 

### Dynamic mappings

With dynamic mapping the global and local address representations are generated automatically
by the NAT router, used when needed and then discarded, this is used to allow a small pool of
global inside addresses to be shared by a large number of local inside addresses.

## IP NAT Unidirectional 

The original NAT protocol was defined in RFC 1631 is the easiest to understand.
* designed to allows hosts on a private network to share public addresses while accessing and internet.
* it's assumed that most inside hosts act as clients and hence initiate transactions
* the NAT capable router when it sees a new transaction initiated tries to assign a global inside address to the IP.
* the responses returned by the server will have dest ip that of the global inside address assigned by the NAT
* when the response reaches the NAT enabled router the address is replaces with the mapped local IP address.
* this sort of NAT only supports requests initiated from the local devices end and doesn't support internet sending a request to the local device.
* In addition to the IP replacements the header checksum and other stuff have to be changed as well.

## IP NAT bidirectional

The problem with traditional NAT is that it can handle only outbound transactions, where 
clients in the private network initiate requests and the public internet server sends back
responses. 

### Asymmetric issue in inbound NAT

The inside network generally knows the IP address of outside devices since their IP addresses
are public but the outside network never gets to know the inside addresses. Unlike in inbound
where the sending device (inside device) knows the address of its destination, the sender in
this case does not know the address of the device.

### Facilitating inbound NAT using DNS 

This can only be used with devices whose addresses are registered with a DNS. Uses __rfc 2694__
* The outside device sends a DNS request using the name of the device on the inside.
* A DNS server for the internal network resolves the name into a local inside local address.
* The inside local address is passed to NAT and used to create a mapping between inside local address of the server and an inside global address.
* When the DNS sends back a name resolution it sends back not the inside local but the global address of the device.
