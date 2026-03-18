"OLE(Object Linking and Embedding) for Process Control"

***Links***:
Python Client: [[Asyncua]]
Node CLI Browser: https://github.com/node-opcua/opcua-commander/tree/b7b805936e6d7068281da2d3fa7f17522ec34a03
## What 
An open standard for implementing different communication standards. usable by any os platform allowing communication between many types of machines. 
- Secure
- Scalable

Based on OLE(Object Linking and Embedding), a Windows COM standard. Originally OPC was only supported by windows.

### Client/Server
#### Server
 Software that provides data to all client applications. OPC Servers are provided by many different vendors. In Stout's machine, the [x90](https://www.br-automation.com/en-us/products/plc-systems/x90-mobile-control-system/) has a provided B&R version of OPCUA server.
 
 #### Client
 Software in any language that connects to the OPCUA server.
 
## Why 
Platform Independent! Supports all platforms.

Before OPC UA every machine needed a driver for communicating with an [[HMI(Human Machine Interface)]] 

Using OPCUA, a standard for communicating between machines is standardized.

Old Communication
![[OldCom.png]]

Communication w/ OPC UA
![[NewCom.png]]



### OPCUA Clients

**[OPCUA Commander](https://github.com/node-opcua/opcua-commander/tree/b7b805936e6d7068281da2d3fa7f17522ec34a03)**

install
```
npm install opcua-commander -g
```

Node Cli
```
opcua-commander -e opc.tcp://localhost:26543 
```
