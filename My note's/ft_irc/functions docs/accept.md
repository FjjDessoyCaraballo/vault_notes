## Synopsis

The `accept()` function is used by a server application to accept an incoming connection request from a client.
- When a client tries to connect to a listening socket (set up with `listen()`), the connection request is queued.
- `accept()` extracts the first connection request from the queue and creates a new socket specifically for communicating with that client.
#### Library
`#include <sys/socket.h`

## Function parameters and return values

`int accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen);`

- `sockfd` The file descriptor of the listening socket (created with `socket()` and set to listening mode with `listening()`);
- `addr` A pointer to a `sockaddr` structure where the address of the connecting client will be stored (e.g., `sockaddr_in` for IPv4 or `sockaddr_in6` for IPv6). Pass `NULL` if you don't need the client's address;
- `addrlen` A pointer to a variable that specifies the size of the `sockaddr` structure. On return, this variable is updated with the actual size of the client address.
## Return values

- Upon **success** it returns a new file descriptor for the socket connected to the client. This socket is used for communication with the client.
- Upon **failure** it returns -1 and sets `errno` appropriately.

### **Common Errors (`errno`)**

1. **`EAGAIN` or `EWOULDBLOCK`**:
    - The socket is marked as non-blocking, and no pending connections are available.
2. **`EBADF`**:
    - The `sockfd` is not a valid file descriptor.
3. **`EINTR`**:
    - The `accept()` call was interrupted by a signal before a connection could be established.
4. **`EINVAL`**:
    - The socket is not listening for connections, or the arguments are invalid.
5. **`EMFILE` or `ENFILE`**:
    - The process or system has reached the maximum number of open file descriptors.

### **How It Works**

1. **Listening Socket**:
    - A socket must be created, bound to an address/port using `bind()`, and marked as listening with `listen()`.
2. **Queue Management**: 
    - Incoming connection requests are queued by the kernel (up to the limit specified in `listen()`).
    - `accept()` retrieves the first pending connection request from this queue.
3. **New Socket Creation**:
    - A new socket is created for the specific client connection.
    - The listening socket (`sockfd`) remains open and can continue to accept additional connections.
4. **Client Address Retrieval**:
    - If `addr` is not `NULL`, the function fills the structure with the client’s address (IP and port) and updates `addrlen` with its size.