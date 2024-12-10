## Synopsis

Host to network long

Converts a 32-bit integer (commonly an IPv4 address) from host byte order to network byte order (big-endian).

In sum: from **LITTLE-ENDIAN** to **BIG-ENDIAN**

`#include <arpa/inet.h>`

## Function and parameters

The function contains only one parameter:

- `uint32_t hostlong` 32-bit unsigned integer in host byte order, such as an IPv4 address.
## Return value

The function returns a 32-bit unsigned integer converted network byte order (big-endian)