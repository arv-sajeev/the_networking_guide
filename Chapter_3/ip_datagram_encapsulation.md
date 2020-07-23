# IP datagram encapsulation and formatting

To help ensure that data packets are transmitted between hosts on an internetwork the data
is encapsulated within a message called an IP datagram.If the message to be transmitted is
too large for the underlying network, it may be fragmented into further IP datagrams the 
receiving device will have to reassemble the original message form the fragmented packets.
These packets are further encapsulated in their respective data-link layer frames which are
specific for each hop.

#### IP datagram encapsulation (From The TCP IP guide)
![IP datagram encapsulation](ip_datagram_encapsulation.png)

## IP datagram general format

The IPV4 format was defined in [RFC 791](https://tools.ietf.org/html/rfc791), the datagrams
are divided into two the header and the payload, the payload carries the actual data to be 
sent the header carries sort of metadata and routing info. The IP datagram does not have 
a footer. The IP header in contrast to the ethernet header is quite large and has a minimum
of 20 bytes.

### IPv-4 datagram format

| Field Name 	| Size (in bytes) 	| Description 					|
|---		|---			|--						|
| Version 	| 4 bits		| Version of IP it is 4 for IPv4 to ensure compatibilty|
| IHL		| 4 bits		| Internet header length specifies header length in byte words, minimum value is 5 for 20 bytes |
| TOS		| 1 byte		| Type of Service USED for QoS and differentiated services|
| TL		| 2 bytes		| Total length specifies total length in bytes including payload and header max size is 65,535 bytes |
| Identification | 2 bytes		| Contains  a 16 bit value that is used to identify fragments that belong to a particular message it is filled even if the packet isn't fragmented| Flags 	| 3 bits	| DF (Option to disable fragmentation) MF (more fragments are yet to come, set to zero for last fragment and unfragmented datagrams) and the other bit is reserved |
| Fragment offset | 13 bits	| If fragmentation occurs it signifies the fragment number within the original message for reassembly |
| TTL	| 1 byte | Time to Live how much the datagram is left to live in terms of hop counts,is decremented at each hop before transmitting it|
| Protocol | 1 byte | Identifies the protocol of the payload |
| Header check sum | 2 bytes | Checksum of only the header, just a simple 16 bit checksum |
| Source address | 4 bytes | 32 bit IP address of the originator of the datagram it is not changed at each hop like in MAC address |
| Destination address | 2 bytes | The IP address of final target destination |
| Options | variable | multiple options can be used |
| Padding | variable | Used to pad the option to make header a multiple of 4 bytes |
| Data | variable | The data to be transmitted or it's fragments|

#### Time to Live Field

This field was originally intended to hold a time value that holds the time left to live, but
it now holds a hop counter that it decrements each hop as it is transmitted from a router.
When the field reaches zero the message is dropped and an ICMP time exceeded message is sent
to inform the source that the message has been dropped. This is done to prevent router loops.

#### Type of Service field

This field is provided to implement QoS details for IP datagram delivery, giving precedence 
and the preferred manner in which they should be delivered.

### IP datagram options

All IP datagrams must include a standard 20-byte header, in addition to this they have the
ability to to add options that provide additional fields and provide flexibilty in how IP 
handles datagrams. Each option has its own subfield format.

#### IP option format

| Option Type | 1 | Option Type :: The 8-bit field is divided into 3 subfields 1 bit for whether the option should be copied for all fragments 2 bits for the option class the popular values are Control and Debugging |
| Option Length | 0 or 1 	|	Size of the entire option field |
| Option data	| 0 or variable |  	For variable length options	|

## IP datagram fragmentation and reassembly

As datagram are passed in between the various routers in an internetwork the data-link layers
along the path might have varying capabilities. The frame size of the IP datagram must match
the maximum transmission unit size. To make sure packets fit the stipulated size the packets
must be fragmented and are reassembled to the original message at each hop.
