# TCP/IP services and Client server operation 

TCP IP is known for its layered structure each layer provides services to the layer above it, The TCP/IP services provided can be divided into two types, services provided to other layers and services provided to the end users directly. TCP and UDP are protocols concerned with encapsulating data and managing connections between devices, they provide services to higher layers. The www is an application of the latter type that uses services provided by lower layers and provides services directly to the user 

## 1. TCP/IP client server structural model

In this model relatively small number of powerful server machines provide services to a much larger number of client hosts.
 
* Two machine that communicate don't use identical software but complementary s/w with one acting as a client and the other acting as a server.

* Doing this the client and server software can be tailored for their different jobs and can be more optimized.

* The client is normally the device that initiates communication or sends a query, the server responds to the query.The rise of more connectivity has led to blurring the lines between client and server 

## 2. Architecture and model

While the OSI model consists of 7 layers the TCP/IP model consists of 4 layers. The physical layer is not considered to be part of the TCP/IP stack 
* The network interface layer - Physical and data-link layer 
* Internet layer - network layer 
* Transport layer - Transport layer 
* Application layer  - Application, presentation, session layer 

Page no- 198 has a figure with the different verticals in each layer 

## 3. Network interface layer protocols 

TCP/IP includes two protocols in the network interface layer 
### 1. SLIP serial line internet protocol
* forms a layer 2 connection between two devices
* an IP datagram is passed down to SLIP, this is broken down to bytes and send one at a time
* after the last byte a special byte value is sent that tells the datagram has ended 11000000
* if the END value occurs within the datagram it is added with an escape character
* SLIP doesn't provide features, no error detection or correction mechanisms, compression etc.

### 2. PPP Point to Point protocol 
* it can actually be considered a suite or protocols 
* replacement for SLIP and is a connection oriented protocol
* it has a better framing mechanism
* has details about which protocol is encapsulated 
* error detection using CRC
* mechanism to negotiate link parameters like MTU
* mechanism to test links before transmission occurs
* authentication, encryption and compression protocols
#### PPP link setup and phases

Before data can be exchanged a link must be set up between two devices, during this setup 
process the devices go through a configuration phase where they negotiate and agree upon the 
different parameters for how data should be passed between them. This function is carried out by the **PPP Link Configuration Protocol**. The LCP might invoke authentication protocols if 
required by the configuration, and Network Control Protocols. The different phases a PPP link
undergoes are

* Link dead phase
* Link establishment phase
* authentication  (using CHAP OR PAP)
* Network layer protocol phase
* Link open phase
* Link termination phase

