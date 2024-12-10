## Synopsis

The `fcntl()` function is versatile system call in Unix-like operating systems, used to manipulate the properties of file descriptors. It is often used for operations such as setting a socket to non-blocking mode, duplicating file descriptors, or managing locks on files.

`#include <fcntl.h>`
## Function and parameters

`int fcntl(int fd, int cmd, ... /* arg */);`

The `fcntl()` function performs various operations on a file descriptor. These operations are determined by the command `cmd` parameter, and some may require an additional argument.

- `fd` The file descriptor to operate on. This can be any file descriptor, including those for files, pipes, or sockets;
- `cmd` The operation to perform. Common commands include:
	- `F_GETFL` get the file descriptors current flags (e.g., blocking or non-blocking mode);
	- `F_SETFL` set the file descriptors flags;
	- `F_GETFD` get the file descriptors flags (close-on-exec);
	- `F_SETFD` set the file descriptor flags (close-on-exec);
- `arg` An optional argument required for some commands, depending on the operation. For example, setting flags with `F_SETFL` requires passing the desired flags as an argument.
## Return values

- Upon success it return a non-negative value, typically `0`, or the requested information (e.g., flags for `F_GETFL`);
- Upon failure it returns `-1` and sets `errno` to indicate the error.

### **Setting a Socket to Non-Blocking Mode**

To set a socket to non-blocking mode:

1. Use `fcntl()` with `F_GETFL` to retrieve the current file descriptor flags.
2. Use `fcntl()` with `F_SETFL` to add the `O_NONBLOCK` flag to the retrieved flags.

Here’s a step-by-step explanation of non-blocking mode:

- In **blocking mode** (default), calls like `accept()` or `recv()` will pause the program until data is available or a connection is established.
- In **non-blocking mode**, these calls return immediately if they cannot proceed, typically setting `errno` to `EAGAIN` or `EWOULDBLOCK`.