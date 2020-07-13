# TCP/IP Internet layer (OSI Network layer) protocols

The IP is the core protocol of the TCP/IP suite in the network layer. It is mainly concerned
about devices that are not on the same physical network but on different networks that maybe
interconnected i.e an internetwork.

## Key characteristics

#### Universally addressed

It should define a mechanism to ensure devices can identify devices that are on completely 
different networks

#### Underlying protocol independent

It should support transmission of data across any type of underlying stack.Ethernet PPP or SLIP

#### Delivered connectionlessly

IP is a connectionless protocol to explicit connection is set up between destination and 
source before transmission begins.

#### Delivered unreliably

The Protocol doesn't keep track of the packets that it sent and the ones that reached, nor
does it provide error protection or flow control.

#### Delivered without acknowledgments

As a product of unreliability and connectionless-ness the protocol doesn't use acknowledgements 

### Success despite limitations

The last three key features may seem like big pitfalls but these are there because these 
functions are left for the higher layers to implement, using the power layering solutions 
for providing reliability and connection when required is done using TCP, UDP and so on in
the transport layer.

## IP functions

It basically is the delivery protocol used for internetwork datagram delivery this can be
divided into.

#### Addressing

Provide a mechanism for host addressing over large inter-networks, unique addresses for all
devices and a structure to facilitate routing.

#### Data encapsulation and Formatting

IP accepts the data from the upper UDP and TCP then encapsulates this to an IP packet before
transmission.

#### Fragmentation and Reassembly

Depending on the maximum frame size for the physical or data-link layer, we might have to
fragment the IP packets to suit this, the fragmentation and reassembly is taken care of by
the IP

#### Routing / Indirect delivery

When an IP is sent to a destination on the same LAN, it is called direct delivery, but for 
the case where the destination is on a distant network that is not directly attached to the
source, it is delivered by routing through multiple intermediate devices.

The functions of IP were carried out by the TCP layer until is was decide to layer it and 
split into IP and TCP in the 1970s


