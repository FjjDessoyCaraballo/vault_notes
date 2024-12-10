## Synopsis

Network to host short (16-bit)

`#include <arpa/inet.h>`

## Function, parameter, and return values

- `uint16_t ntohs(uint16_t netshort);`
- `uint16_t netshort` a 16-bit unsigned integer in network byte order;
- The function returns a 16-bit unsigned integer converted to host byte order.

## Usage

When you receive a port number from the network, it will be in network byte order. Use `ntohs()` to convert it back to host byte order for proper interpretation.
