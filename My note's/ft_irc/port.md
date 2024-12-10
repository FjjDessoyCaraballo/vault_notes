# What is a port?

A port is a logical endpoint associated with a specific process or service on a computer. It is used to identify and manage communication between devices in a network. Ports allow a single device to run multiple network services simultaneously by directing incoming and outgoing data to the correct application.

## What should I know about ports?

1. Relationship with IP addresses:
	1. A port is a part of the transport layer in the networking stack;
	2. Together with an IP address, a port forms a socket that uniquely identifies a network connection. For example, `192.168.1.1:80` refers to an HTTP service on a device with the IP address `192.168.1.1`;
2. Numerical range
	1. Ports are 16-bit numbers. Check more bellow in [[port#Length of a port]];
3. Purpose of ports
	1. ports help direct network traffic to the appropriate application or service on a device. For example:
			- Web servers typically listen on port 80 (HTTP) or port 442 (HTTPS)
			- Email servers might use port 25 (SMTP);
4. TCP and UDP:
	1. Ports are used by TCP and UDP
	2. TCP provides reliable, connection-oriented communication, while UDP offers faster, connectionless communication.
	3. The same port number can be used for both TCP and UDP but corresponds to different services;

If you venture into analogy, it is a door into a house. The house being the device in a network, the IP address is the house address, and the IP + port `192.168.1.1:80` is the address with instructions to which door you can use. After all, you don't want strangers coming through back doors.

## Length of a port

A port number is **16 bits long**, which means it can range from **0 to 65535**.

Port numbers are used in networking to identify specific processes or services on a device. They are divided into three ranges:

1. **Well-known ports**: 0 to 1023 (reserved for commonly used services, such as HTTP on port 80, FTP on port 21).
2. **Registered ports**: 1024 to 49151 (used for specific applications that are not well-known but are registered with the IANA).
3. **Dynamic or private ports**: 49152 to 65535 (used for temporary or ephemeral connections, often assigned dynamically by the operating system).