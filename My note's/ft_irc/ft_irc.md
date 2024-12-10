
# General guidelines

An IRC (Internet Relay Chat) server needs to:

1. **Accept Connections from Clients**:  
    Clients (IRC applications) connect to the server to send messages and receive updates about chatrooms or other users.  
    Sockets provide the mechanism to **listen for incoming connections** and establish a communication channel with each client.
    
2. **Enable Reliable Communication**:  
    IRC servers typically use TCP (Transmission Control Protocol), which ensures:
    
    - Data is delivered in order.
    - Missing packets are retransmitted.
    - A reliable connection is established between the client and server.  
        Sockets abstract the complexities of TCP and allow you to work with the data as a stream.
3. **Support Multiple Connections**:  
    An IRC server can serve many clients simultaneously. Sockets allow you to:
    
    - Create a main listening socket for incoming connections.
    - Spawn individual sockets for each client connection.
    - Use techniques like **multi-threading** or **non-blocking I/O** to handle multiple clients concurrently.
4. **Interoperability with IRC Clients**:  
    IRC clients follow the IRC protocol (defined in RFC 1459 and its updates). Sockets allow your server to:
    
    - Parse and respond to protocol-specific commands like `JOIN`, `PRIVMSG`, `QUIT`, etc.
    - Maintain real-time communication with clients.

# Allowed functions

- [[socket]]
- close
- setsockopt
- getsockname
- getprotobyname
- gethostbyname
- getaddrinfo
- freeaddrinfo
- [[bind]]
- connect
- [[listen]]
- accept
- [[htons]]
- htonl
- ntohs
- ntohl
- inet_addr
- inet_ntoa
- send
- recv
- signal
- lseek
- fstat
- fcntl
- poll

### **Comparison Table of [[htons]], [[htonl]], [[ntohs]], [[ntohl]]**

|**Function**|**Input** (Host/Network Byte Order)|**Output** (Host/Network Byte Order)|**Bit Size**|**Purpose**|
|---|---|---|---|---|
|`htons()`|Host|Network|16 bits|Convert port numbers to network order.|
|`htonl()`|Host|Network|32 bits|Convert IPv4 addresses to network order.|
|`ntohs()`|Network|Host|16 bits|Convert port numbers to host order.|
|`ntohl()`|Network|Host|32 bits|Convert IPv4 addresses to host order.|

**Use Cases**:

- `htons()`/`htonl()`: For sending data.
- `ntohs()`/`ntohl()`: For receiving data.