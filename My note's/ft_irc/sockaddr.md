sockaddr is a generic structure defined in `<sys/socket.h>` that acts as a universal type for all socket address structures. Its role is to provide a common interface for handling different address families (e.g. IPv4, IPv6, or Unix domain sockets).

You can typically use a specialized versions like `sockaddr_in` (IPv4) or `sockaddr_in6` (IPv6) and cast them to `sockaddr`. The casting works because the `sockaddr` structure is designed to accommodate all address types.
## Definition for IPv4 addresses

Define the proper library

```c
#include <netinet/in.h>
```

```c
struct sockaddr_in {
    sa_family_t    sin_family; // Address family (AF_INET)
    uint16_t       sin_port;   // Port number (network byte order)
    struct in_addr sin_addr;   // IPv4 address
    char           sin_zero[8]; // Padding (not used)
};

```

- `sin_family` always set to `AF_INET` for IPv4 sockets;
- `sin_port` port number (converted to network byte order with `htons()`);
- `sin_addr` structure  holding the IPv4 address. Use `INADDR_ANY` to bind to all interfaces;
- `sin_zero` padding to match the size of the `sockaddr`

### Step 1 - Creating the socket

```cpp
int sockfd = socket(AF_INET, SOCK_STREAM, 0);
```

This is merely casting `server_addr` into `sockaddr*`.

### Step 2 - Preparing an address with `sockaddr_in`

```cpp
struct sockaddr_in server_addr;
server_addr.sin_family = AF_INET;
server_addr.sin_port = htons(6667); // arbitrary port number (byte order)
server_addr.sin_addr.s_addr = INADDR_ANY; // bind to all network interfaces
```

In this step we are mainly filling the struct variables with address and port. After this, we can provide [[bind]] with these.

### step 3 - Cast for compatibility

```cpp
bind(sockfd, (struct sockaddr *)&server_addr, sizeof(server_addr));
```

## Definition for IPv6 addresses

```c
#include <netinet/in.h>
```

```c
struct sockaddr_in6 {
    sa_family_t     sin6_family;   // Address family (AF_INET6)
    in_port_t       sin6_port;     // Port number (network byte order)
    uint32_t        sin6_flowinfo; // Traffic class and flow information
    struct in6_addr sin6_addr;     // IPv6 address
    uint32_t        sin6_scope_id; // Scope ID (interface index or zone index)
};
```

- `sin6_family` specifies the address family. For IPv6 this field is set to `AF_INET6`;
- `sin6_port` contains the port number in **network byte order** (big-endian). Use `htons()` or `ntohs()` to convert between host and network byte order;
- `sin6_flowinfo` specifies IPv6 traffic class and flow label. It's used for the Quality of Service (QoS) or advanced networking features;
- `sin6_addr` A struct `in6_addr` that contains the IPv6 address which is usually 128 bits. Refer to [[sockaddr#`sin6_addr` struct definition]] for the definition of the struct;
- `sin6_scope_id` specifies the scope of the address. For link-local addresses (starting with `FE80::`) this field is used to specify the network interface index.
### step 1

```cpp
int sockfd = socket(AF_INET6, SOCK_STREAM, 0);
```

We create a file descriptor `sockfd` to create a socket from the `socket()` function.
### step 2

```cpp
struct sockaddr_in6 server_addr6;
server_addr6.sin6_family = AF_INET6;
server_addr6.sin6_port = htons(6667); // arbitrary port
server_addr6.sin6_addr = in6addr_any; // bind to all network interfaces
```

In this step we are mainly filling the struct variables with address and port. After this, we can provide [[bind]] with these.

### step 3

```cpp
bind(sockfd, (struct sockaddr *)&server_addr6, sizeof(server_addr6));
```

This is merely casting `server_addr6` into `sockaddr*`.

## `sin6_addr` struct definition

```c
struct in6_addr {
    unsigned char s6_addr[16]; // IPv6 address (128 bits)
};
```