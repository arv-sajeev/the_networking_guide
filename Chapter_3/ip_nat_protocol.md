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
