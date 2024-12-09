# synopsis

Creates an endpoint for communication by opening  a fd that refers to the endpoint.

`#include <sys/socket.h>`

## Function and parameters

`int socket( int domain, int type, int protocol);`

- `domain` specifies communication domain (ipv4 `AF_INET` or `AF_INET6` ipv6 for us);
- `type` socket type. Specifies the communication semantics. Some of the common values:
  1. `SOCK_STREAM` connection-oriented communication (e.g. TCP);
  2. `SOCK_DGRAM` connectionless communication (e.g. UDP);
  3. `SOCK_RAW` provides raw network protocol access;
- `protocol` specifies specific protocol to be used with the socket. It can be set automatically with `0`, but for guaranteed effect we should define what is required by the subject: `IPPROTO_TCP` (TCP v4/6)

## Return value

Upon success, the function returns a file descriptor for the new socket that is returned.

Upon error, it returns -1 and `errno` is set to indicate the error.

### **How Your IRC Server Will Use Sockets**

Here’s a typical flow for an IRC server using sockets:

1. **Create a Socket**:  
    Use the `socket()` function to create a listening socket.
    
2. **Bind to a Port**:  
    Use the [[bind]] function to assign the socket to a specific port (e.g., 6667, the default for IRC servers).
    
3. **Listen for Connections**:  
    Use the [[listen]] function to allow the socket to accept incoming client connections.
    
4. **Accept Connections**:  
    Use the `accept()` function to create a new socket for each client that connects to the server.
    
5. **Send and Receive Data**:  
    Use functions like `send()` and `recv()` to handle messages exchanged between the server and clients.
    
6. **Close the Connection**:  
    Use the `close()` function to release resources when a client disconnects or when shutting down the server.