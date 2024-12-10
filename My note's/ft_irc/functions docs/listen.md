## Synposis

The [[listen]] function transitions a socket from its initial state (created by [[socket]]) into a state where it can accept incoming connection requests. It effectively marks the socket as a listening socket for server applications.

listen for connections on a socket. Without the listen function, a [[socket]] cannot accept connections using the [[accept]] function.

`#include <sys/socket.h`
## Function and parameters

`int listen(int sockfd, int backlog);`

- `sockfd` The file descriptor of the socket to be marked as a listening socket. This socket must already be bound to an address an port using the [[bind]] function.
- `backlog` The maximum number of pending connection requests the kernel should queue for the socket. If more connection requests arrive than the backlog allows, additional requests are either ignored or refused, depending on the system configuration. The actual limit might be capped by the system's maximum queue size (e.g., `proc/sys/net/core/somaxconn` on linux).
## Return values

- 0 upon success;
- -1 upon failure and `errno` is set to indicate the error.

### **Common Errors (`errno`)**

1. **`EADDRINUSE`**:
    
    - The address is already in use, and the socket cannot be reused.
    - Use `setsockopt()` with `SO_REUSEADDR` to allow address reuse.
2. **`EBADF`**:
    
    - The file descriptor `sockfd` is invalid or not an open socket.
3. **`ENOTSOCK`**:
    
    - `sockfd` does not refer to a socket.
4. **`EOPNOTSUPP`**:
    
    - The socket type does not support listening (e.g., `SOCK_DGRAM`).
5. **`EINVAL`**:
    
    - The socket is not properly bound or is already in a listening state.

### **How `listen()` Works**

1. **Setup Phase**:
    
    - After creating a socket with [[socket]] and binding it to an address with [[bind]], the server calls [[listen]] to prepare the socket for incoming connections.
2. **Backlog Queue**:
    
    - The kernel maintains a queue of incoming connection requests.
    - The `backlog` parameter defines the maximum number of pending connections that can wait in this queue before being processed by [[accept]].
3. **Accepting Connections**:
    
    - Once the socket is in the listening state, the server can call `accept()` to handle connection requests one by one.