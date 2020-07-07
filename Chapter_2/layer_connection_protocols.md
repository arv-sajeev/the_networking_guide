# TCP/IP network Interface 

The second layer of the OSI model is the data-link layer this corresponds to the 
TCP/IP network interface layer, The third layer is the network layer and is also called the 
internet layer.

To connect these two layers there are a bunch of protocols that are about half way in between
the 2nd and 3rd layers sort of like a 2.5 layer.The protocols in this interface are -

## Address Resolution Protocol

Communication on an internetwork proceeds sending data at layer three using a network layer
address (IP address), but the actual transmission of data occurs at layer two using the 
data-link layer address (MAC address), so there exists to addresses to identify a device on 
a network and we need a way to translate b/w these two layers, ARP is responsible for this

As per OSI model our aim is to make sure the logical functions of each layer are completely
separate and the lower layer details are hidden. So why do we need this mapping between 
different layer addresses. 

### Addressing at Layer 2 and Layer 3

* the addresses in L-2 are meant for directly connected devices on the same network like LAN or WAN
* the L-3 addresses are meant for indirectly as well as directly connected devices
* IP addresses are too high level and consists of multiple hops for finally reaching the destination 
* MAC addresses on the other hand are immediate next hop addresses


### General Address Resolution methods

#### Direct mapping

* used to map or get the l-2 address from the l-3 address directly
* highly efficient but has limitations on the size of the l2 size
* for e.g Arc-net used the final 8 bits of the IP addr
* but since the number of devices is very high the MAC address size will be very large
* it produces high linkage between the layers making it very inflexible

#### Dynamic address resolution 

* it uses a series of enquiries and responses to reach an understanding to which l2 is assigned to which l3
* it requires quite a lot of overhead processing.
* `who is` request are sent and flooded the request is processed by all that receive it 
* only the assigned one replies
* caching is used to improve efficiency 
* the cache has to be refreshed frequently, used the LRU cache

## TCP/IP ARP

It is fully functional dynamic resolution protocol, used to match IP addresses to it's
underlying l-2 addresses. Originally developed for ethernet and now has been generalised.
The new IPv6 used the Neighbor Discovery protocol which does basically the same thing

* uses the RFC 826
* the basic operation consists of a request/response pair of transmission of the local network
* the transmits a broadcast containing information about the destination 

### ARP message types

* Request  - the sender is the device that needs to resolve an IP
* Response - the sender is the device that has the IP specified address

### Process

1. Check id in cache
1. generates request message
1. broadcasts request message
1. Local devices process message
1. Destination device generates reply
1. Destination updates its cache
1. Destination send reply
1. Source processes reply
1. Source updates cache

## ARP caching 

ARP being a dynamic protocol requires the constant exchange of messages on the network for 
address resolutions, this can consume the network bandwidth so we need to cache entries and
responses.

* Static ARP cache entries - address resolutions manually added to the table, kept in the cache permanently until manually modified
* Dynamic ARP cache entries are added to the cache by the software using messages received and is refreshed periodically

### Cache entry expiration 

Entries have to be changed when
* The devices h/w changes
* The devices ip address changes
* The device is removed or stops functioning 

## Proxy ARP

When to devices are separated by a router or are "2 hops" apart, the first device cannot get
the address resolution for the dest with a simple arp implementation. 
* Here proxy arp comes into picture 
* The router in between responds to the requests of the src since it is connected to dest
* it also know dest's address and can route packets there
* the router responds with it's own address
* when it receives packets with destination as dest it routes it using info on the arp table
* this make's it almost transparent to the hosts
knows the address of dest since it's entry is in it's arp table. The router sends the src it's

# Address resolution for IP multicast addresses

We need a method to convert the IP multicast group address to addresses of the devices in 
the data link layer. We could maybe convert the IP to individual unicast transmissions but
this would be very inefficient.

## Direct mapping technique for IEEE 802 multicast MAC addresses

IP tries to make use of the underlying protocols multicast addressing properties, in spite of
using dynamic arp protocol it uses simple direct mapping between IP multicast groups and MAC multicast groups.

### The IEEE 802 addressing system
* one of the most popular data-link layer addressing system's used in ethernet
* addresses have 48 bits i.e 6 bytes
* the upper 24 bits are assigned as OUI or Organizationally Unique Identifier assigned to different organizations
* the lower 24 bits are used for specific devices

For the direct mapping multicast technique the OUI for multicast addresses id defined by the
IANA as ___01 00 5E___ this is followed by a 0 and can represent 23 bits of the IP multicast
address. This will be directly mapped from the bottom 23 bits of the IP multicast address.

This however doesn't guarantee the uniqueness of multicast address. 32 IP's can be mapped
to the same MAC address.

# TCP/IP address resolution for IPv6

The functions of ARP and ICMP and other protocols have been combined in to a new protocol suite called the ND or ___Neighbor discovery___ protocol.
* if underlying protocol supports multicast, multicast is used rather than broadcast for neighbor solicitation messages (like arp request)
* the replies made are called neighbor advertisement messages.

# Reverse Address Resolution 

Some devices when they start up may have a valid MAC addresses but may not know what it's
IP address is. Devices like those that don't have disks or memory to maintain state and IP.
These devices then create a RARP request and if a dedicated rarp server is on the network 
they will receive a response.

RARP is outdated and protocols like BOOTP and DHCP are used instead in the TCP\IP stack.
