sockaddr is a generic structure defined in `<sys/socket.h>` that acts as a universal type for all socket address structures. Its role is to provide a common interface for handling different address families (e.g. IPv4, IPv6, or Unix domain sockets).

You can typically use a specialized versions like `sockaddr_in` (IPv4) or `sockaddr_in6` (IPv6) and cast them to `sockaddr`. The casting works because the `sockaddr` structure is designed to accommodate all address types.
#### Definition

```c
struct sockaddr {
    sa_family_t sa_family;   // Address family (e.g., AF_INET, AF_INET6)
    char        sa_data[14]; // Address data (varies by family)
};
```

