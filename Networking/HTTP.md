
### REST (Representational State Transfer)
Rest is a definition of a standard for networking transferring invented by [[Roy Fielding]]
### HTTP (Hypertext Transfer Protocol)
HTTP uses a [[TCP]] connection.
HTTP is an implementation of REST based on its core principles. The basis of the internet, HTTP has a few defining features.
1. **HTTP is connectionless**. After making a request, the client disconnects from the server. When the response is ready, the server re-establishes connection
2. **HTTP can deliver any sort of data**
3. **HTTP is stateless**. The client and server know about eachother for the duration they are connected.

#### History
HTTP was designed mainly to fetch HTML documents.
It was written well enough that eventually became the primary form of all data communication.

#### Client/Server Paradigm
The HTTP communication is the following:
- A client first establishes a TCP/IP connection to a server
- Once establish, a REQUEST HTTP message is sent.
- The client then disconnects
- The server prepares a response
- The server then establishes a connection to the client over TCP/IP
- The server send a HTTP RESPONSE message
- The server disconnects

#### HTTP Message Format
1. Start Line
2. Headers
3. Body

All contain plaintext, though the body may contain binary data. 
![[Pasted image 20240206141935.png]]

**Request Message**
Method: GET/POST/PUT/DELETE
URI: Readable characters pathing to the requested file.
HTTP Version