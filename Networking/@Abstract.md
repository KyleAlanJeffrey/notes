## OSI Model
***The basis of all intercommunication***
![[Pasted image 20240404130304.png]]
1. Physical Layer: Physical and Encoding
	- Radiowave
	- Copperwire
	- Fiber Optic
	- [[CAN (Controller area network)]]
2. Datalink: Framing 
	- Ethernet
	- PPP
	- [[CAN (Controller area network)]]
3. Network Layer
	- 
4. Transport Layer
	- [[TCP]]
	- [[UDP]]
5. Session Layer
	- 
6. Presentation Layer
	- 
7. Application Layer
	- [[Modbus]]
	- [[HTTP]]
	- [[DNS]]
	- [[FTP]]
	- [[SMTP]]

## Digital Communication
Some notes from: https://www.youtube.com/watch?v=XaGXPObx2Gs&list=PLowKtXNTBypH19whXTVoG3oKSuOcw_XeW

How do you send information?:
- Voltages over a copper wire
- Light through a fiber optic cable
- Using radio waves


### Frames in Networking
-> Need a way to frame data to know how to align bytes of information

- HDLC(High Level Data-limit Control)
- Ethernet: Has 0 voltage for many bits then 56 bits of alternating 1's and 0's then a Frame Delimeter 




Ethernet Frame:
![[Pasted image 20240218121104.png]]
Common Ether types (2 bytes):
- 0800: IP
- 0806: ARP (Address Resolution Protocoo)

**ARP (Address Resolution Protocol)**
This is used to determine the HW Address of an IP Address. This is broadcast to the whole network. 



### DHCP (Dynamic Host Configuration Protocol)
A communication by which a DHCP sever will assign a client its DNS server, local ip address, and router ip address.



# Networking

## Ports

a port is non-physical. It is a logical connection thats used to exchange information.

**Ports range from 0 - 65535**
**Ports are maintained by the Internet Assigned Numbers Authority (IANA)**
**They exist in 3 categories:**
- 0-1023 are System or Well-known ports
	- HTTP Server -> 80
	- FTP Server -> 21
- 1024-49151 are User or Registered Ports
	- Adobe Server -> 1102
	- Microsoft SQL Server -> 1433
	- Oracle -> 1527
- 49152 - 65535 are Dynamic or private ports
	- Clients will use these ports
