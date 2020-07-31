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

## IPSec Implementation methods

Three different variation of IPSec are defined in its RFC 2401, they are classified on the 
basis of whether the version used in IPv6 or v4 
