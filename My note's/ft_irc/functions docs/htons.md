## Synposis

`htons()` stands for **Host to Network Short**. Its primary purpose is to convert a 16-bit number (typically a port number) from the host's byte order (endiannesss) to **network byte order**, which is big-endian.

#### **Byte Order**
- Host byte order: different systerms represent multi-byte numbers differently:
	- little-endian: least significant byte is stored first (e.g., x86 systems);
	- big-endian: most significant byte is stored first (e.g., some older systems);
- Network byte order: to ensure consistency in communication, all networking protocols use big-endian format. This is also known as **network byte order**.

`htons()` ensures that numbers are correctly converted to big-endian format before being transmitted over the network.

`#include <arpa/inet.h>`
## Function and parameters

`uint16_t htons(uint16_t hostshort);`

- `hostshort` a 16-bit unsigned integer (typically a [[Port]] number) in host byte order. The value to be converted.

## Return value

- It returns the converted value