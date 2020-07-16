# IP addressing

IP is mainly is responsible for delivering messages between devices that are not on the
same physical networks but on separate interconnected networks that maybe multiple hops 
apart. Hence the most major feature of IP is the addressing scheme that is robust enough to
handle such a large network and yet still identify each device and provide a method to route
to the device efficiently. The IP addressing scheme evolved continuously from inception from
simple methods to classful, classless sub-netting and various other concepts. 
Yet the basic concepts remain almost the same.

---

### IP addressing overview and fundamentals

The functions of an IP address are-

### Network interface identification  

Like a street address the IP address provides a unique identification of the interface 
between the device and the network.

### Routing  

When the source and dest ip are not on the same network they must be delivered indirectly 
via intermediate systems this is called routing.

### Address Uniqueness 

Each IP address on a single internetwork must be unique. Note that the uniqueness is only 
for the given network it is part of.

### Network specificity of IP address

Since IP addresses actually represent the network it is on and the device the IP should be
specific for each network as well. This means that if the device moves to a new network it's
IP will change as well.

### IP address datagram delivery issues

In ethernet the MAC address is all the information that is required to send data between 
devices. The IP address on the other hand will only represent the final delivery point of 
the datagram. It has to be routed.

### Private and Public IP addresses

On a private network a single organization controls the assignment of the addresses, they maintain the uniqueness. The public network has organizations to register and allocate addresses

### IP address configuration 

IP address can be configured manually to a static IP that doesn't change. This is okay for 
small networks but gets really tough to control as the size of the network grows. For large
networks configuration is done dynamically using protocols like BOOTP and DHCP.

### Unicast Multicast and Broadcast

The IP addressing scheme must service all three types of addressing.


Network interface rather than device because one device may have multiple network interfaces.
The structure of the IP address is also special that it enables routing. Some special hosts,
may have more than one IP address if they are multihomed i.e. connected to more than one network.

--- 


## IP address size and notation 

The IP address is simply a 32 bit binary number, to make it more readable we represent it
as each byte of the number in its decimal form separated by dots.

### IP address space

With the address being 32 bits wide, this gives an address space of 2^32. The legacy systems
of IP waster much of the address space for e.g all numbers with 127 as first byte are loop back giving 2^24 loopback addresses. Techniques like CIDR and NAT have been used to make more
efficient use of the address space.

### IP address structure.

The 32 bits IP address structure consists of two parts. 
* Network id - the left-most bits are used to identify the network the device belongs to.
* Host id    - the remainder of the bits are used to identify the host on the network.

The length of Network ID and Host ID vary according to the type of network. The network ID
being a part of the IP address is a major part in how it is routed. The routers look at the
network ID to decide if the destination IP is on the same network. The further routing 
decisions are made based on the network ID.

The network id can be thought of like the area code in a phone number but unlike phone nos
the length of the phone number and area code can vary.

### Some special addresses

* if we use an IP address with a given network ID and host id as all 1's this is a broadcast to the entire specified network
* full 1's is i.e 255.255.255.255 is a limited broadcast i.e broadcast within it's own network
* if IP address with network ID all zeros then it is send to the destination IP on the same
network.

### Splitting of the IP address

The network ID and host ID are usually represented individually with the gaps after the 
split filled with 0's. The split need not occur at exact octet intervals but happens
bitwise.

---

## IP addressing categories and IP address adjuncts

The splitting of the IP address as discussed above depends on the scheme used. Many 
different schemes have evolved and we use the CIDR scheme right now.

### Conventional addressing (Classful)

This was the original ip addressing scheme, it allows splits only at octet boundaries.
The addresses are then divided into classes depending on where the address splits and
how many bits the host and network addresses have. The range for the network address
is also fixed.

### Subnetted Classful addressing

In addition to the two tier network host division of the IP address. A few bits from the 
network ID is are used as a subnet identifier. Introducing the concept of a subnetwork
this is the further split is indicated by a subnet mask.

### Classless addressing 

In the classless system the classes of the original IP scheme are no used. The division of 
the network ID and host ID can occur at any point. The split point is supplied with the 
address a prefix length or network prefix which is the network ID size.

## IP address registration 

* The IANA was initially in charge of allocating IP addresses and other numbers
* In the 90's the ICANN started which took over and also did DNS registration 
* Now we use the CIDR hierarchical addressing scheme the IANA no longer assigns directly but delegates them to regional authorities.
* ISP's obtain blocks of IP addresses for use by end users like us.

---

## IP "Classful" Addressing

When the internet first started they never thought that it would be used by normal people 
and there main requirements were just to produce different classes of IP addresses for the
various size of organizations.

There are 5 classes in the classful addressing system.

| Class | Fraction of total IP space | Number of Net id bits | Number of Host ID bits | Intended used|
|---	|---			     |---		     |---		      |---	     |
| A	| 50%   | 8  | 24 | Unicast addressing for very large organizations with millions of hosts connected to it|
| B	| 25%   | 16 | 16 | Unicast addressing for medium to large organization with thousands of hosts connected |
| C 	| 12.5% | 24 | 8  | Unicast addressing for smaller organizations for a max 256 hosts |
| D     | 6.25% | na | na | IP multicasting |
| E 	| 6.25% | na | na | For experimental use | 

