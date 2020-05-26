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
* SLIP serial line internet protocol
..* Provides basic TCP/IP functionality by creating a layer two connection between two devices in a serial line.

* PPP Point to Point protocol 
Prov

