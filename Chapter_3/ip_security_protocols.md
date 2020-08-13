# IP Security Protocols

The IP protocol provides an efficient way for routing and addressing, but it does not provide
any mechanism for ensuring the authenticity and privacy of the data that is passed over the 
internet. All data in IP network can be intercepted by anyone who has physical access to the
network.

* all methods to address security are focussed on the higher layers of the stack like SSL etc
* these can't be generalized easily because they are specific for different applications
* security at network layer could provide security to all applications, this lead to IPSec

## IPSec services and functions

The IPSec like IP is not a single protocol but a set of services and protocols that provide a
security solution for an IP network, its functions are.
* Encryption of user data for privacy
* Authentication of integrity of data
* Negotiate security algorithms between hosts and reach a consensus
* tunnel and transport mode for different security needs.

## IPSec core protocols

The functions of IPSec suite of protocols can be listed as
* Negotiate and agree on a set of protocols to use so they can understand each other
* exchange cryptographic keys
* send data to each other using agreed upon keys and protocols 

The two main pieces are a pair of core protocols

### IP Authentication Header

* Provides authentication services
* allows recipient to check whether the sender is the one that is supposed to be in packet
* the data has not lost its integrity or been tampered with

### Encapsulating Security Payload

* The IP-AH ensures integrity and authenticity
* the ESP is responsible for privacy, encrypts the payload

## IPSec support components

### Encryption/Hashing algorithms

* This specifies the exact mechanism use for encryption
* MD5 and SHA1

### Security policies and associations

* IPSec allows flexibility letting devices decide how they want to implement security
* the negotiation process and associations set up are handled by

### Key exchange framework

* For two devices to exchange encrypted info they need to be able to exchange keys 
* The IIKE or internet key exchange handles this key exchange process
 
---

## IPSec Implementation methods

Three different variation of IPSec are defined in its RFC 2401, they are classified on the 
basis of whether the version used in IPv6 or v4, and whether the IPSec is to be programmed
into all hosts on a network or just to a few devices.

### End host implementation methods

Putting IPSec into all host devices provides most flexibility and security with true end
to end security. This implies any connection between any two devices on the network is 
secure. The trade-off is that lots of work has to be done to get the implementation running
in each hop, and increases processing overhead as well.

### Router implementation

IPSec is implemented only between certain routers. This option has less overhead and setting 
up costs. But for can be used when we know certain paths are secured by other  means.

## IPSec Architectures

Classifying architectures based on how we plan to integrate IPSec into the protocol stack.

### Integrated architecture

Under Ideal circumstances it would be best to completely integrate it into IP itself. But
this is not possible as it would require us to update the software in each intermediate machine.
IPv6 is already designed to support IPsec, on the other hand IPv4 has not such provision

### Bump in the stack architecture

In this mode the IPSec is made a separate interface between the data link layer and IP layer 
The implementation can be fitted to any IP device, but requires lot of duplication of effort 
over the different hosts.

### Bump in the wire

A hardware device that provides IPSec services. Is added in between the two devices 
Removes IPSec encapsulation for incoming packets and adds it for outgoing packets.

---

## IPSec modes

IPSec modes determine how the core protocols AH and ESP add to the security by
adding to the header and other fields of the datagram. The choice of mode 
changes the locations where the modifications are made by the protocols.

### Transport mode

In transport mode the protocol protects the message passed to IP from the transport layer.
The datagram is processed by AH/ESP and headers are added to the datagram from TCP/UDP before
IP header is added.

* when used in transport mode, the core protocols are applied only on the IP payload.
* requires the implementation to be integrated into the protocol stack

### Tunnel mode

In tunnel mode the core protocols are applied on the entire IP datagram including IP header
after all the IP headers and other fields have been applied to it.

* the core protocols are applied only on the entire IP datagram
* either the BITS or BITW architecture can be used.
* tunnel mode is more prevalent with widespread use in VPN

--- 

## IPSec Security associations and database

A device with IPSec will have to exchange info with multiple devices. The different peers
mah have different security requirements and capabilities, this has to be negotiated and 
agreed upon. Extra overhead goes into setting up the different exchanges. To handle this 
policies, associations and a database are used.

* Security policy 	- is a rule programmed into the IPSec that tells how to process different datagrams from different devices. Whether of not it needs to processed by IPSec etc.
* Security associations - is a set of security information that specifies a particular kind of secure connection. They are unidirectional 

### Selector

It is the rule set that determines which device belongs to which SA,
for e.g a range of address values combined with another value.
Security associations are defined by a set of three parameters called a triple
* Security parameter index - a 32 bit number for uniquely identifying a particular SA for a given dest device
* IP dest address - address of the device with whom the SA is established.
* Security protocol identifier - specifies whether the SA is for AH or ESP, they are treated differently

---

## IPSec Authentication header

AH is a protocol that provided authentication of either all or part of the contents of the 
datagram by adding a header that is calculated based on the values of the datagram.

We use a special hashing algorithm known to everyone, with a key only known to the source and
the destination. AH performs the computation and puts the result into a special header (ICV) 
with other fields for transmission. The destination devices performs the same calculation 
using the key they share and can find out whether the datagram has been tampered with.

### IPv6 Authentication header placement and linking 

The AH is inserted into the IP datagram as an extension header, following the normal IPv6 
rules. It is linked to the previous header putting into its next header the assigned value 
for the AH header. The AH header then links to the next extension header or the transport layer header using its next header field.
* In transport mode AH is placed into the main IP header before the dest options, but after any other extension headers
* IN tunnel mode it appears as an extension header of the new IP datagram that encapsulates the original one being tunneled.


|	 0 	| 	1 	| 	2 	| 	3 	|
|---		|---		|---		|---		|
| Next header	| Payload len	| Reserved	|	''	|
|Security	| parameter 	| index		|	''	|
|		|	Sequence| number	|		|
|	Auth	|	Auth	|   Auth	| 	Auth	|
|Data		|	 Data	|  Data		| Data		|
|		| Integrity 	| check value	|		|


* Next header 	- a 1 byte to contain the protocol number of the next header after AH
* Payload len 	- measures length of the AH itself
* Reserved    	- Not used set to zeroes
* SPI   	- a 32 bit value that when combined with dest address and SP type identifies the security association
* Sequence no 	- This is a counter field that is initialized to zero when SA is set up and increments for each datagram sent. Use to uniquely identify datagrams and prevent replay attacks
* Authentication data - the rest is the result of the hashing algorithm.

### Encapsulating Security payload fields

* Unlike the AH the ESP packages its fields in a very different way.
* ESP header  	- contains the SPI and Sequence number, comes before the encrypted data
* ESP trailer 	- This section contains padding used to align encrypted data, it is processed by encryption as well. In contains a next header that points to the header after ESP header.
* ESP Auth data	- Contains and ICV like in AH.

---

## IPSec key Exchange

The IKE protocol is used to exchange information, mainly the key for encoding  required for 
secure communication. It is used to allow IPSec enabled devices to share there SA's and setup
their SAD.
 	
