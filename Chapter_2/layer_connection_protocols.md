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

### TCP/IP ARP

It is fully functional dynamic resolution protocol, used to match IP addresses to it's
underlying l-2 addresses. Originally developed for ethernet and now has been generalised.
The new IPv6 used the Neighbor Discovery protocol which does basically the same thing

* uses the RFC 826
* the basic operation consists of a request/response pair of transmission of the local network
* the transmits a broadcast containing information about the destination 

#### ARP message types
* Request  - the sender is the device that needs to resolve an IP
* Response - the sender is the device that has the IP specified address

#### Process
1. Check id in cache
1. generates request message
1. broadcasts request message
1. Local devices process message
1. Destination device generates reply
1. Destination updates its cache
1. Destination send reply
1. Source processes reply
1. Source updates cache
