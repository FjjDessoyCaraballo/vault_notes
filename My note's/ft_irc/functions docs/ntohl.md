## Synopsis

The function converts a 32-bit integer (commonly an IPv4 address) from network byte order (big-endian) to host byte order.

`#include <arpa/inet.h>`
## Function, parameters, and return values

- `uint32_t ntohl(uint32_t netlong);`
- `uint32_t netlong` a 32-bit integer in network byte order;
- The function returns a 32-bit integer converted to host byte order.