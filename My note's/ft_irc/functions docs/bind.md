## Synopsis

bind a name to a socket.

`#include <sys/socket.h>`

## Function and paramaters 

`int bind(int sockfd, const struct sockaddr *addr, socklen_t addrlen);`

- `sockfd` socket file descriptor obtained with the method [[socket]], binding the socket to the address and port;
- `addr (pointer to struct sockaddr)` 
- `addr` length of address structure;